{
  "nodes": [
    {
      "parameters": {
        "rule": {
          "interval": [
            {
              "field": "minutes",
              "minutesInterval": 10
            }
          ]
        }
      },
      "type": "n8n-nodes-base.scheduleTrigger",
      "typeVersion": 1.3,
      "position": [
        0,
        0
      ],
      "id": "68a82e74-c806-443c-b744-ba16cde11c11",
      "name": "Schedule Trigger"
    },
    {
      "parameters": {
        "method": "POST",
        "url": "https://google.serper.dev/search",
        "authentication": "genericCredentialType",
        "genericAuthType": "httpHeaderAuth",
        "sendBody": true,
        "specifyBody": "json",
        "jsonBody": "{\n  \"q\": \"\\\"NF Academy\\\" OR \\\"Nurul fikri Academy\\\"\",\n  \"gl\": \"id\"\n}",
        "options": {}
      },
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 4.4,
      "position": [
        192,
        -144
      ],
      "id": "9e227277-b984-44eb-b4a5-0483b8da463b",
      "name": "NFA",
      "credentials": {
        "httpHeaderAuth": {
          "id": "cmy98dWIlxtURUAF",
          "name": "Header Auth account"
        }
      }
    },
    {
      "parameters": {
        "method": "POST",
        "url": "https://google.serper.dev/search",
        "authentication": "genericCredentialType",
        "genericAuthType": "httpHeaderAuth",
        "sendBody": true,
        "specifyBody": "json",
        "jsonBody": "{\n  \"q\": \"\\\"BISA AI\\\"\", \"gl\": \"id\"\n}",
        "options": {}
      },
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 4.4,
      "position": [
        192,
        0
      ],
      "id": "f532b891-f1e7-4638-8944-a5cc5f34c65f",
      "name": "Bisa Ai",
      "credentials": {
        "httpHeaderAuth": {
          "id": "cmy98dWIlxtURUAF",
          "name": "Header Auth account"
        }
      }
    },
    {
      "parameters": {
        "method": "POST",
        "url": "https://google.serper.dev/search",
        "authentication": "genericCredentialType",
        "genericAuthType": "httpHeaderAuth",
        "sendBody": true,
        "specifyBody": "json",
        "jsonBody": "{\n  \"q\": \"\\\"Vinix 7\\\"\", \"gl\": \"id\"\n}",
        "options": {}
      },
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 4.4,
      "position": [
        192,
        144
      ],
      "id": "0dd8d8f3-5af9-4f47-b2b6-722deebbee74",
      "name": "Vinix7",
      "credentials": {
        "httpHeaderAuth": {
          "id": "cmy98dWIlxtURUAF",
          "name": "Header Auth account"
        }
      }
    },
    {
      "parameters": {
        "jsCode": "// Fungsi untuk mengambil data secara aman dari node search\nconst getOrganicData = (nodeName) => {\n  try {\n    const results = $(nodeName).all();\n    // Mengambil array 'organic' dari hasil Serper API\n    return results[0].json.organic || [];\n  } catch (e) {\n    return []; // Jika node gagal, berikan array kosong agar workflow tidak stop\n  }\n};\n\nconst nfaResults = getOrganicData('NFA');\nconst bisaResults = getOrganicData('BISA AI');\nconst vinixResults = getOrganicData('Vinix7');\n\n// Gunakan DateTime.now() dari Luxon (bukan $now.format)\nconst currentTime = DateTime.now().toFormat('yyyy-MM-dd HH:mm');\n\n// Gabungkan dan berikan label brand ke setiap berita\nconst finalData = [\n  ...nfaResults.map(i => ({ json: { ...i, brand: 'NF Academy', processedAt: currentTime } })),\n  ...bisaResults.map(i => ({ json: { ...i, brand: 'BISA AI', processedAt: currentTime } })),\n  ...vinixResults.map(i => ({ json: { ...i, brand: 'Vinix 7', processedAt: currentTime } }))\n];\n\nreturn finalData;\n"
      },
      "type": "n8n-nodes-base.code",
      "typeVersion": 2,
      "position": [
        432,
        0
      ],
      "id": "5fe7a56e-012d-4788-b62b-213fb7e16cf6",
      "name": "gabungkan data"
    },
    {
      "parameters": {
        "jsCode": "// Mengambil seluruh item dari node sebelumnya\nconst allItems = $input.all();\nconst total = allItems.length;\n\n// Menghitung mention per brand secara total\nconst counts = {\n  nfa: allItems.filter(i => i.json.brand === \"NF Academy\").length,\n  bisa: allItems.filter(i => i.json.brand === \"BISA AI\").length,\n  vinix: allItems.filter(i => i.json.brand === \"Vinix 7\").length\n};\n\n// Menghitung Share of Voice (SOV)\nconst sov = {\n  nfa: total > 0 ? ((counts.nfa / total) * 100).toFixed(1) : 0,\n  bisa: total > 0 ? ((counts.bisa / total) * 100).toFixed(1) : 0,\n  vinix: total > 0 ? ((counts.vinix / total) * 100).toFixed(1) : 0\n};\n\n// Menggabungkan seluruh teks berita menjadi satu blok teks untuk AI\nlet combinedText = \"\";\nallItems.forEach(item => {\n  combinedText += `[${item.json.brand}] ${item.json.title}: ${item.json.snippet}\\n\\n`;\n});\n\n// PENTING: Mengembalikan HANYA SATU objek (bukan array)\nreturn {\n  metrics: {\n    processedAt: DateTime.now().toFormat('yyyy-MM-dd HH:mm'),\n    total_mentions: total,\n    breakdown: counts,\n    share_of_voice: sov,\n    dashboard_url: \"https://docs.google.com/spreadsheets/d/19yDBpx981bYwOzIKD7oxHG80YdfDqY_ZUmVyCIYbXNU/edit\"\n  },\n  text_for_ai: combinedText\n};\n\n"
      },
      "type": "n8n-nodes-base.code",
      "typeVersion": 2,
      "position": [
        624,
        0
      ],
      "id": "0bdfabd9-2265-40fa-a8e2-28e9aa58323b",
      "name": "menyiapkan teks AI"
    },
    {
      "parameters": {
        "promptType": "define",
        "text": "={\n  \"prompt\": \"Lakukan analisis kompetitif berdasarkan DATA METRICS berikut:\\n- Total Mentions: {{ $json.metrics.total_mentions }}\\n- NF Academy: {{ $json.metrics.breakdown.nfa }} mention ({{ $json.metrics.share_of_voice.nfa }}%)\\n- BISA AI: {{ $json.metrics.breakdown.bisa }} mention ({{ $json.metrics.share_of_voice.bisa }}%)\\n- Vinix 7: {{ $json.metrics.breakdown.vinix }} mention ({{ $json.metrics.share_of_voice.vinix }}%)\\n\\nDATA MENTAH:\\n{{ $json.text_for_ai }}\\n\\nTugas Anda:\\n1. Mengapa Share of Voice [Brand Tertinggi] lebih besar?\\n2. Berikan skor reputasi 1-10 untuk NF Academy dibandingkan kompetitor berdasarkan kualitas snippet tersebut.\"\n}",
        "messages": {
          "messageValues": [
            {
              "message": "Anda adalah seorang Pakar Strategi Bisnis dan Analis Intelijen Kompetitif senior.  Tugas Anda adalah melakukan audit mendalam terhadap performa brand berdasarkan data metrics dan snippet teks yang diberikan.  Gunakan logika berpikir kritis untuk: 1. Menjelaskan faktor pendorong dominasi pasar (Share of Voice) dari brand yang memimpin. 2. Mengevaluasi kualitas sentimen dan reputasi NF Academy dibandingkan kompetitornya. 3. Memberikan penilaian objektif (1-10) berdasarkan kredibilitas informasi dalam data mentah.  Berikan analisis yang strategis, tajam, dan profesional dalam format laporan singkat."
            }
          ]
        },
        "batching": {}
      },
      "type": "@n8n/n8n-nodes-langchain.chainLlm",
      "typeVersion": 1.9,
      "position": [
        832,
        0
      ],
      "id": "219e8f59-5aa8-49fd-8cca-cdd9fdb37d6e",
      "name": "Basic LLM Chain"
    },
    {
      "parameters": {
        "operation": "append",
        "documentId": {
          "__rl": true,
          "value": "1-FMN1dfar6BnIQxsfpjsPR9JnF8p9OydOqiCdBBiV-8",
          "mode": "list",
          "cachedResultName": "workflow analisis",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1-FMN1dfar6BnIQxsfpjsPR9JnF8p9OydOqiCdBBiV-8/edit?usp=drivesdk"
        },
        "sheetName": {
          "__rl": true,
          "value": "gid=0",
          "mode": "list",
          "cachedResultName": "Sheet1",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1-FMN1dfar6BnIQxsfpjsPR9JnF8p9OydOqiCdBBiV-8/edit#gid=0"
        },
        "columns": {
          "mappingMode": "defineBelow",
          "value": {
            "Tanggal": "={{ $('menyiapkan teks AI').item.json.metrics.processedAt }}",
            "NF Academy": "={{ $('menyiapkan teks AI').item.json.breakdown.nfa }}",
            "BISA AI": "={{ $('menyiapkan teks AI').item.json.breakdown.bisa }}",
            "Vinix 7": "={{ $('menyiapkan teks AI').item.json.breakdown.vinix }}"
          },
          "matchingColumns": [],
          "schema": [
            {
              "id": "Tanggal",
              "displayName": "Tanggal",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": false
            },
            {
              "id": "NF Academy",
              "displayName": "NF Academy",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": false
            },
            {
              "id": "BISA AI",
              "displayName": "BISA AI",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": false
            },
            {
              "id": "Vinix 7",
              "displayName": "Vinix 7",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": false
            },
            {
              "id": "Total Mention",
              "displayName": "Total Mention",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": false
            }
          ],
          "attemptToConvertTypes": false,
          "convertFieldsToString": false
        },
        "options": {
          "cellFormat": "USER_ENTERED"
        }
      },
      "type": "n8n-nodes-base.googleSheets",
      "typeVersion": 4.7,
      "position": [
        1136,
        0
      ],
      "id": "8e68b79e-fa1d-495c-a309-f947f7ea9480",
      "name": "Append row in sheet",
      "credentials": {
        "googleSheetsOAuth2Api": {
          "id": "1i4CpejrRiWAa25G",
          "name": "Google Sheets account 3"
        }
      }
    },
    {
      "parameters": {
        "html": "<!DOCTYPE html>\n<html lang=\"id\">\n<head>\n  <meta charset=\"UTF-8\" />\n  <meta name=\"viewport\" content=\"width=device-width, initial-scale=1.0\"/>\n  <title>Laporan Strategi Bisnis & Intelijen Kompetitif</title>\n\n  <style>\n    :root {\n      --orange: #FF6B35;\n      --blue: #2E5AAC;\n      --blue-light: #4A7DCC;\n      --gray-bg: #f8f9fa;\n      --text-dark: #333;\n      --text-light: #6c757d;\n    }\n\n    * {\n      margin: 0;\n      padding: 0;\n      box-sizing: border-box;\n    }\n\n    body {\n      font-family: Arial, Helvetica, sans-serif;\n      line-height: 1.6;\n      color: var(--text-dark);\n      background: #ffffff;\n    }\n\n    .container {\n      max-width: 1000px;\n      margin: 0 auto;\n      padding: 24px;\n    }\n\n    header {\n      background: linear-gradient(135deg, var(--blue), var(--blue-light));\n      color: white;\n      padding: 48px 24px;\n      text-align: center;\n      border-radius: 0 0 14px 14px;\n    }\n\n    header h1 {\n      font-size: 28px;\n      font-weight: bold;\n      margin-bottom: 10px;\n    }\n\n    header p {\n      font-size: 15px;\n      opacity: 0.95;\n    }\n\n    .badge {\n      display: inline-block;\n      margin-top: 12px;\n      background: var(--orange);\n      padding: 6px 14px;\n      border-radius: 20px;\n      font-size: 13px;\n      font-weight: bold;\n    }\n\n    section {\n      background: #ffffff;\n      margin: 32px 0;\n      padding: 28px;\n      border-radius: 12px;\n      border: 1px solid #eee;\n    }\n\n    h2 {\n      font-size: 22px;\n      color: var(--blue);\n      margin-bottom: 18px;\n      padding-bottom: 8px;\n      border-bottom: 2px solid var(--orange);\n    }\n\n    h3 {\n      font-size: 18px;\n      color: var(--blue);\n      margin: 18px 0 10px;\n    }\n\n    p {\n      margin-bottom: 12px;\n    }\n\n    ul, ol {\n      margin-left: 22px;\n    }\n\n    li {\n      margin-bottom: 10px;\n    }\n\n    .highlight {\n      background: #fff4e6;\n      padding: 2px 6px;\n      border-radius: 4px;\n      font-weight: bold;\n      color: #d35400;\n    }\n\n    /* Table */\n    table {\n      width: 100%;\n      border-collapse: collapse;\n      margin-top: 16px;\n    }\n\n    th {\n      background: var(--blue);\n      color: white;\n      padding: 12px;\n      font-size: 14px;\n    }\n\n    td {\n      padding: 12px;\n      border-bottom: 1px solid #eee;\n      font-size: 14px;\n      vertical-align: top;\n    }\n\n    .brand-bisa { background: #fff7f1; }\n    .brand-nf { background: #f1f6ff; }\n    .brand-vinix { background: #fafafa; color: #999; }\n\n    .score-bisa { color: var(--orange); font-weight: bold; }\n    .score-nf { color: var(--blue); font-weight: bold; }\n\n    .bar {\n      height: 18px;\n      border-radius: 10px;\n      margin: 6px 0 14px;\n      background: #ddd;\n      overflow: hidden;\n    }\n\n    .bar span {\n      display: block;\n      height: 100%;\n    }\n\n    .bar-bisa span { width: 53.3%; background: var(--orange); }\n    .bar-nf span { width: 46.7%; background: var(--blue); }\n\n    footer {\n      margin-top: 40px;\n      text-align: center;\n      font-size: 13px;\n      color: var(--text-light);\n    }\n\n    @media print {\n      section { page-break-inside: avoid; }\n    }\n  </style>\n</head>\n\n<body>\n\n<header>\n  <div class=\"container\">\n    <h1>📊 Laporan Strategi Bisnis & Intelijen Kompetitif</h1>\n    <p>Analisis Share of Voice (SoV) & Reputasi Digital</p>\n    <div class=\"badge\">📅 07 Januari 2026</div>\n  </div>\n</header>\n\n<div class=\"container\">\n\n  <section>\n    <h2>📌 Ringkasan Eksekutif</h2>\n    <p>\n      Dalam percakapan digital terbatas (<strong>15 mention</strong>),\n      <span class=\"highlight\">BISA AI</span> unggul tipis dengan\n      <strong>53.3% Share of Voice</strong>, sementara\n      <strong>NF Academy</strong> berada di <strong>46.7%</strong>.\n    </p>\n\n    <p><strong>BISA AI (53.3%)</strong></p>\n    <div class=\"bar bar-bisa\"><span></span></div>\n\n    <p><strong>NF Academy (46.7%)</strong></p>\n    <div class=\"bar bar-nf\"><span></span></div>\n  </section>\n\n  <section>\n    <h2>📢 Analisis Share of Voice</h2>\n\n    <h3>🤖 BISA AI</h3>\n    <ul>\n      <li>Fokus topikal AI & Data Science</li>\n      <li>Promosi agresif dan edukatif</li>\n      <li>Akses kursus gratis + sertifikasi</li>\n    </ul>\n\n    <h3>🎓 NF Academy</h3>\n    <ul>\n      <li>Konten dominan profil statis</li>\n      <li>Minim diskusi & CTA viral</li>\n    </ul>\n  </section>\n\n  <section>\n    <h2>⭐ Skor Reputasi</h2>\n    <table>\n      <tr>\n        <th>Brand</th>\n        <th>Skor</th>\n        <th>Kelebihan</th>\n        <th>Kelemahan</th>\n      </tr>\n      <tr class=\"brand-bisa\">\n        <td><strong>BISA AI</strong></td>\n        <td class=\"score-bisa\">8.0 / 10</td>\n        <td>Relevan, gratis, online</td>\n        <td>Branding generik</td>\n      </tr>\n      <tr class=\"brand-nf\">\n        <td><strong>NF Academy</strong></td>\n        <td class=\"score-nf\">6.5 / 10</td>\n        <td>Lokasi fisik, B2B</td>\n        <td>Konten kaku</td>\n      </tr>\n      <tr class=\"brand-vinix\">\n        <td><strong>Vinix 7</strong></td>\n        <td>0 / 10</td>\n        <td>—</td>\n        <td>Tidak terdeteksi</td>\n      </tr>\n    </table>\n  </section>\n\n  <section>\n    <h2>💡 Strategi Rekomendasi untuk NF Academy</h2>\n    <ol>\n      <li>Aktifkan konten sosial & instruktur</li>\n      <li>Tonjolkan keunggulan kelas tatap muka</li>\n      <li>Gunakan promosi berbasis hasil nyata</li>\n    </ol>\n  </section>\n\n  <footer>\n    <p>© 2026 — Laporan Strategi Bisnis & Intelijen Kompetitif</p>\n    <p>Data publik & analisis sosial media (Jan 2026)</p>\n  </footer>\n\n</div>\n\n</body>\n</html>\n"
      },
      "type": "n8n-nodes-base.html",
      "typeVersion": 1.2,
      "position": [
        1344,
        0
      ],
      "id": "922244dd-b454-47ca-bcb9-580a744a299e",
      "name": "HTML"
    },
    {
      "parameters": {
        "method": "POST",
        "url": "https://api.pdfshift.io/v3/convert/pdf",
        "sendHeaders": true,
        "headerParameters": {
          "parameters": [
            {
              "name": "X-API-Key",
              "value": "sk_092369370f68959492ad1ce5b7dbf29ef65adbbc"
            }
          ]
        },
        "sendBody": true,
        "bodyParameters": {
          "parameters": [
            {
              "name": "source",
              "value": "={{ $json.html }}"
            }
          ]
        },
        "options": {
          "response": {
            "response": {
              "responseFormat": "file"
            }
          }
        }
      },
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 4.4,
      "position": [
        1552,
        0
      ],
      "id": "493b5904-8334-4888-ad65-85e7274daf19",
      "name": "HTTP Request"
    },
    {
      "parameters": {
        "operation": "sendDocument",
        "chatId": "1535237765",
        "binaryData": true,
        "additionalFields": {
          "caption": "=📊 *Laporan Intelijen Kompetitif - 07 Januari 2026*\n\n🔹 BISA AI unggul tipis dengan SoV 53.3%  \n🔹 NF Academy perlu optimasi konten dinamis  \n🔹 Vinix 7: belum terdeteksi — masalah awareness!\n\n📎 Lampiran: PDF lengkap analisis & rekomendasi strategis.\n\n",
          "fileName": "Lapran Kompetitor - 10 April 2026"
        }
      },
      "type": "n8n-nodes-base.telegram",
      "typeVersion": 1.2,
      "position": [
        1904,
        0
      ],
      "id": "13f7c0ce-47e1-411f-bd64-af26f5acd1fd",
      "name": "Send a document",
      "webhookId": "aec4d9f5-8c50-4fab-ba9a-cd2eee8ac37a",
      "credentials": {
        "telegramApi": {
          "id": "UeW4rIKFaGuH61DK",
          "name": "bot renjeun"
        }
      }
    },
    {
      "parameters": {
        "model": "openai/gpt-oss-120b:free",
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.lmChatOpenRouter",
      "typeVersion": 1,
      "position": [
        768,
        208
      ],
      "id": "6f461625-0691-4595-8f7c-1a33688e2566",
      "name": "OpenRouter Chat Model",
      "credentials": {
        "openRouterApi": {
          "id": "690Ovy8cCHBHAqHt",
          "name": "awa"
        }
      }
    },
    {
      "parameters": {
        "assignments": {
          "assignments": [
            {
              "id": "326f2b6d-fe1f-4772-9fb6-635b4117f1d7",
              "name": "data",
              "value": "={{ $binary.data }}",
              "type": "binary"
            }
          ]
        },
        "includeOtherFields": true,
        "options": {
          "stripBinary": true
        }
      },
      "type": "n8n-nodes-base.set",
      "typeVersion": 3.4,
      "position": [
        1728,
        0
      ],
      "id": "a26f0027-5f66-4eb8-9a7e-d6595798d57c",
      "name": "Edit Fields"
    }
  ],
  "connections": {
    "Schedule Trigger": {
      "main": [
        [
          {
            "node": "NFA",
            "type": "main",
            "index": 0
          },
          {
            "node": "Bisa Ai",
            "type": "main",
            "index": 0
          },
          {
            "node": "Vinix7",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "NFA": {
      "main": [
        [
          {
            "node": "gabungkan data",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Bisa Ai": {
      "main": [
        [
          {
            "node": "gabungkan data",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Vinix7": {
      "main": [
        [
          {
            "node": "gabungkan data",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "gabungkan data": {
      "main": [
        [
          {
            "node": "menyiapkan teks AI",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "menyiapkan teks AI": {
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
            "node": "Append row in sheet",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Append row in sheet": {
      "main": [
        [
          {
            "node": "HTML",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "HTML": {
      "main": [
        [
          {
            "node": "HTTP Request",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "HTTP Request": {
      "main": [
        [
          {
            "node": "Edit Fields",
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
    },
    "Edit Fields": {
      "main": [
        [
          {
            "node": "Send a document",
            "type": "main",
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
