{
  "nodes": [
    {
      "parameters": {
        "pollTimes": {
          "item": [
            {
              "mode": "everyMinute"
            }
          ]
        },
        "triggerOn": "specificFolder",
        "folderToWatch": {
          "__rl": true,
          "value": "1C9A5FfI5pwJP-aExhYDkBxH_6K_xC7iX",
          "mode": "list",
          "cachedResultName": "Upload CV",
          "cachedResultUrl": "https://drive.google.com/drive/folders/1C9A5FfI5pwJP-aExhYDkBxH_6K_xC7iX"
        },
        "event": "fileUpdated",
        "options": {}
      },
      "type": "n8n-nodes-base.googleDriveTrigger",
      "typeVersion": 1,
      "position": [
        0,
        0
      ],
      "id": "2203f7e6-305f-429c-9569-4ab2d8e75ee8",
      "name": "Google Drive Trigger",
      "credentials": {
        "googleDriveOAuth2Api": {
          "id": "39QtVPz9h44W7oq4",
          "name": "Google Drive account 2"
        }
      }
    },
    {
      "parameters": {
        "operation": "Convert from PDF",
        "url": "=https://drive.google.com/file/d/1nvy46j-7JXWz0-DiMvMOR_CIIcgzelQh/view?usp=drivesdk",
        "advancedOptions": {}
      },
      "type": "n8n-nodes-pdfco.PDFco Api",
      "typeVersion": 1,
      "position": [
        416,
        0
      ],
      "id": "72031af0-4868-4d09-9e00-d2e4c9f1bda7",
      "name": "PDFco Api",
      "credentials": {
        "pdfcoApi": {
          "id": "K4dm1VFOibZ1fGp2",
          "name": "pke akun salwabila12720"
        }
      }
    },
    {
      "parameters": {
        "jsCode": "// 1. Ambil data teks langsung dari body PDFco\nlet html = $node[\"PDFco Api\"].json[\"body\"] || \"\";\n\n// 2. Proses Pembersihan Regex\nhtml = html\n  .replace(/<script[\\s\\S]*?<\\/script>/gi, '')\n  .replace(/<style[\\s\\S]*?<\\/style>/gi, '')\n  .replace(/<[^>]+>/g, ' ') // Hapus tag HTML\n  .replace(/&nbsp;/g, ' ')\n  .replace(/\\s+/g, ' ') // Normalisasi spasi\n  .trim();\n\nreturn [{\n  json: {\n    clean_text: html\n  }\n}];"
      },
      "type": "n8n-nodes-base.code",
      "typeVersion": 2,
      "position": [
        624,
        0
      ],
      "id": "ea6ecac6-2115-434d-a31f-acf03f3e2ad1",
      "name": "Clean HTML"
    },
    {
      "parameters": {
        "promptType": "define",
        "text": "Anda adalah Penganalisis CV yang ahli dalam merekrut Tenaga Pengajar IT (Instruktur/Trainer).\n\nAnalisis teks di bawah dan hasilkan HANYA output JSON dengan struktur yang SAMA PERSIS seperti ini:\n\n{\n  \"it_keywords\": [],\n  \"teaching_keywords\": [],\n  \"category\": {\n    \"devops\": [],\n    \"backend\": [],\n    \"frontend\": [],\n    \"cybersecurity\": [],\n    \"cloud\": [],\n    \"networking\": []\n  },\n  \"it_difficulty_score\": \"\",\n  \"teaching_score\": \"\",\n  \"summary\": \"\"\n}\n\nAturan Wajib:\n- \"it_keywords\": Maksimal 10 istilah teknis IT terkuat (cth: \"Python\", \"Kubernetes\").\n- \"teaching_keywords\": Maksimal 5 istilah terkait mengajar (cth: \"mengajar\", \"dosen\", \"trainer\", \"pelatihan\", \"instruktur\").\n- \"category\": Isi kategori IT berdasarkan \"it_keywords\" atau pengalaman kerja.\n- \"it_difficulty_score\": Skor 1-10 untuk kompleksitas teknis IT kandidat.\n- \"teaching_score\": Skor 1-10 untuk pengalaman mengajar/melatih kandidat.\n- \"summary\": Ringkasan 2 kalimat yang menggabungkan kemampuan teknis DAN pengalaman mengajarnya.\n- Jika tidak ada data untuk sebuah array (seperti \"teaching_keywords\"), gunakan array kosong []. Jangan menebak.\n\nSekarang analisis teks ini:\n\n{{ $json.clean_text }}\n\nOutput harus menggunakan Bahasa Indonesia.\n\nAnda adalah Penganalisis CV yang ahli dalam merekrut Tenaga Pengajar IT...\n\n(Instruksi JSON kamu...)\n\nBerikut adalah teks CV yang harus dianalisis:\n{{ $node[\"Clean HTML\"].json[\"clean_text\"] }}",
        "batching": {}
      },
      "type": "@n8n/n8n-nodes-langchain.chainLlm",
      "typeVersion": 1.9,
      "position": [
        832,
        0
      ],
      "id": "cff190cf-8e07-4077-be22-9b01a1f83e5c",
      "name": "Basic LLM Chain"
    },
    {
      "parameters": {
        "jsCode": "// 1. Ambil teks mentah dari AI (OpenRouter)\nconst rawText = $json.text;\n\n// 2. Bersihkan karakter aneh dan perbaiki koma ganda yang sering muncul di model kecil\nlet cleanedText = rawText\n  .replace(/,,/g, ',')      // Perbaiki koma ganda\n  .replace(/,\\s*}/g, '}')   // Hapus trailing comma pada objek\n  .replace(/,\\s*]/g, ']');  // Hapus trailing comma pada array\n\n// 3. Temukan blok JSON (mengambil kurung kurawal terluar)\nconst jsonMatch = cleanedText.match(/\\{[\\s\\S]*\\}/);\n\nif (!jsonMatch) {\n  throw new Error(\"AI tidak memberikan format JSON. Coba jalankan ulang.\");\n}\n\nconst jsonString = jsonMatch[0];\n\n// 4. Ubah menjadi objek JSON\ntry {\n  const jsonData = JSON.parse(jsonString);\n  return [{ json: jsonData }];\n} catch (error) {\n  // Jika gagal, coba hapus karakter baris baru yang mungkin merusak parsing\n  try {\n    const fallbackData = JSON.parse(jsonString.replace(/\\n/g, \" \"));\n    return [{ json: fallbackData }];\n  } catch (e) {\n    throw new Error(\"Gagal parsing JSON: \" + error.message);\n  }\n}"
      },
      "type": "n8n-nodes-base.code",
      "typeVersion": 2,
      "position": [
        1184,
        0
      ],
      "id": "a007d5ca-1e6b-402a-9c42-5974830b39e2",
      "name": "Parse JSON from AI"
    },
    {
      "parameters": {
        "jsCode": "const data = $json;\nconst safeArray = (x) => Array.isArray(x) && x.length > 0 ? x.join(\", \") : \"-\";\nconst cat = data.category || {};\n\nconst msg = `\n📌 *Keyword IT*\n${safeArray(data.it_keywords)}\n\n🎓 *Keyword Mengajar*\n${safeArray(data.teaching_keywords)}\n\n📂 *Kategori*\nDevOps: ${safeArray(cat.devops)}\nBackend: ${safeArray(cat.backend)}\nFrontend: ${safeArray(cat.frontend)}\nSecurity: ${safeArray(cat.cybersecurity || cat.security)}\nCloud: ${safeArray(cat.cloud)}\nNetworking: ${safeArray(cat.networking)}\n\n⭐ *Skor Teknis IT:* ${data.it_difficulty_score || \"0\"}\n⭐ *Skor Mengajar:* ${data.teaching_score || \"0\"}\n\n📝 *Ringkasan:*\n${data.summary || \"-\"}\n`;\n\nreturn [{ json: { telegram_text: msg } }];"
      },
      "type": "n8n-nodes-base.code",
      "typeVersion": 2,
      "position": [
        1392,
        0
      ],
      "id": "808c53fe-db5e-435c-b97e-6620453fc375",
      "name": "Format Output untuk Telegram"
    },
    {
      "parameters": {
        "chatId": "1535237765",
        "text": "={{ $json.telegram_text }}",
        "additionalFields": {}
      },
      "type": "n8n-nodes-base.telegram",
      "typeVersion": 1.2,
      "position": [
        1552,
        0
      ],
      "id": "e1e96e63-afe9-47a6-b8ac-f8bd3f0afa2d",
      "name": "Send a text message",
      "webhookId": "a9552538-cad7-45b8-b041-d43a13cc5cd7",
      "credentials": {
        "telegramApi": {
          "id": "n7cxOzcieENzevJa",
          "name": "mark lee"
        }
      }
    },
    {
      "parameters": {
        "operation": "share",
        "fileId": {
          "__rl": true,
          "value": "={{ $json.id }}",
          "mode": "id"
        },
        "permissionsUi": {
          "permissionsValues": {
            "role": "reader",
            "type": "anyone"
          }
        },
        "options": {}
      },
      "type": "n8n-nodes-base.googleDrive",
      "typeVersion": 3,
      "position": [
        208,
        0
      ],
      "id": "39233f2f-522e-4e45-9394-d08bed9b58ba",
      "name": "Share file",
      "credentials": {
        "googleDriveOAuth2Api": {
          "id": "39QtVPz9h44W7oq4",
          "name": "Google Drive account 2"
        }
      }
    },
    {
      "parameters": {
        "model": "liquid/lfm-2.5-1.2b-thinking:free",
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.lmChatOpenRouter",
      "typeVersion": 1,
      "position": [
        864,
        304
      ],
      "id": "71d2dff7-5625-4439-9c90-125dcc0c8ff7",
      "name": "OpenRouter Chat Model",
      "credentials": {
        "openRouterApi": {
          "id": "690Ovy8cCHBHAqHt",
          "name": "awa"
        }
      }
    }
  ],
  "connections": {
    "Google Drive Trigger": {
      "main": [
        [
          {
            "node": "Share file",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "PDFco Api": {
      "main": [
        [
          {
            "node": "Clean HTML",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Clean HTML": {
      "main": [
        [
          {
            "node": "Basic LLM Chain",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Basic LLM Chain": {
      "main": [
        [
          {
            "node": "Parse JSON from AI",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Parse JSON from AI": {
      "main": [
        [
          {
            "node": "Format Output untuk Telegram",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Format Output untuk Telegram": {
      "main": [
        [
          {
            "node": "Send a text message",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Share file": {
      "main": [
        [
          {
            "node": "PDFco Api",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "OpenRouter Chat Model": {
      "ai_languageModel": [
        [
          {
            "node": "Basic LLM Chain",
            "type": "ai_languageModel",
            "index": 0
          }
        ]
      ]
    }
  },
  "pinData": {},
  "meta": {
    "templateCredsSetupCompleted": true,
    "instanceId": "f9c216ef2c5ce3632c1ddcbc770aee702ab0e63a38eea8ec506f2d08fc35dd05"
  }
}
