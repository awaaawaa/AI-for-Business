{
  "nodes": [
    {
      "parameters": {
        "rule": {
          "interval": [
            {}
          ]
        }
      },
      "type": "n8n-nodes-base.scheduleTrigger",
      "typeVersion": 1.3,
      "position": [
        0,
        0
      ],
      "id": "3d0428ba-b4ec-45b8-9d26-4a9ec41afaed",
      "name": "Schedule Trigger"
    },
    {
      "parameters": {
        "documentId": {
          "__rl": true,
          "value": "1NnJhEgKX9vnbJrhTAXRFBWLws4svurphOXM0V5MVFaw",
          "mode": "list",
          "cachedResultName": "Copy of Dummy Rekonsiliasi",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1NnJhEgKX9vnbJrhTAXRFBWLws4svurphOXM0V5MVFaw/edit?usp=drivesdk"
        },
        "sheetName": {
          "__rl": true,
          "value": "gid=0",
          "mode": "list",
          "cachedResultName": "Sheet1",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1NnJhEgKX9vnbJrhTAXRFBWLws4svurphOXM0V5MVFaw/edit#gid=0"
        },
        "options": {}
      },
      "type": "n8n-nodes-base.googleSheets",
      "typeVersion": 4.7,
      "position": [
        192,
        0
      ],
      "id": "9b248f33-6361-4a99-9f86-66fb9240e33f",
      "name": "data internal",
      "credentials": {
        "googleSheetsOAuth2Api": {
          "id": "1i4CpejrRiWAa25G",
          "name": "Google Sheets account 3"
        }
      }
    },
    {
      "parameters": {
        "operation": "download",
        "fileId": {
          "__rl": true,
          "value": "1JRjpRs-NUeh7LrPbdMgUv5tHy78NJLTb",
          "mode": "list",
          "cachedResultName": "Dummy Rekonsiliasi - Sheet2.csv",
          "cachedResultUrl": "https://drive.google.com/file/d/1JRjpRs-NUeh7LrPbdMgUv5tHy78NJLTb/view?usp=drivesdk"
        },
        "options": {}
      },
      "type": "n8n-nodes-base.googleDrive",
      "typeVersion": 3,
      "position": [
        192,
        144
      ],
      "id": "c6db203c-7aef-4c05-bfa9-cba2accc342e",
      "name": "data bank",
      "credentials": {
        "googleDriveOAuth2Api": {
          "id": "39QtVPz9h44W7oq4",
          "name": "Google Drive account 2"
        }
      }
    },
    {
      "parameters": {
        "options": {}
      },
      "type": "n8n-nodes-base.extractFromFile",
      "typeVersion": 1.1,
      "position": [
        400,
        144
      ],
      "id": "6ac10cba-5f47-4cea-b5ab-2e4297b33749",
      "name": "Extract from File"
    },
    {
      "parameters": {
        "jsCode": "// CODE NODE: CLEAN INTERNAL DATA (REVISI)\nconst results = [];\n\nfor (const item of $input.all()) {\n  const json = item.json;\n\n  // 1. Filter Tipe Transaksi\n  const tipe = json['Tipe Transaksi'];\n  if (tipe !== 'Pembayaran' && tipe !== 'Pengeluaran' && tipe !== 'Penerimaan') {\n    continue; \n  }\n\n  // 2. Bersihkan Tanggal (Hapus spasi & format ulang)\n  // Asumsi format di CSV/Sheet: DD/MM/YYYY\n  const rawDate = (json['Tanggal Transaksi'] || '').toString().trim();\n  const dateParts = rawDate.split('/');\n  // Pastikan date valid\n  if (dateParts.length !== 3) continue;\n  \n  const cleanDate = `${dateParts[2]}-${dateParts[1]}-${dateParts[0]}`;\n\n  // 3. PENTING: Bersihkan Angka dari titik (.) atau koma (,)\n  // Kita ubah jadi string dulu, hapus semua yang BUKAN angka, baru parse\n  const rawAmount = (json['Jumlah (IDR)'] || '0').toString();\n  const cleanAmount = parseInt(rawAmount.replace(/[^0-9]/g, ''));\n\n  // 4. Buat Match Key\n  const matchKey = `${cleanDate}_${cleanAmount}`;\n\n  results.push({\n    json: {\n      ...json,\n      clean_date: cleanDate,\n      clean_amount: cleanAmount,\n      match_key: matchKey,\n      sumber: 'Internal'\n    }\n  });\n}\n\nreturn results;\n"
      },
      "type": "n8n-nodes-base.code",
      "typeVersion": 2,
      "position": [
        400,
        0
      ],
      "id": "c1bbbeec-2417-42a0-a1d4-e1c96d3ed54a",
      "name": "filter baris"
    },
    {
      "parameters": {
        "jsCode": "// CODE NODE: CLEAN BANK DATA (REVISI)\nconst results = [];\n\nfor (const item of $input.all()) {\n  const json = item.json;\n\n  // 1. Bersihkan Tanggal\n  const rawDate = (json['Tanggal Bank'] || '').toString().trim();\n  const dateParts = rawDate.split('/');\n  if (dateParts.length !== 3) continue;\n\n  const cleanDate = `${dateParts[2]}-${dateParts[1]}-${dateParts[0]}`;\n\n  // 2. PENTING: Bersihkan Angka (Hapus titik ribuan Rupiah)\n  const rawAmount = (json['Jumlah (IDR)'] || '0').toString();\n  // Regex ini menghapus apa saja yang bukan angka (termasuk titik/koma)\n  const cleanAmount = parseInt(rawAmount.replace(/[^0-9]/g, ''));\n\n  // 3. Buat Match Key\n  const matchKey = `${cleanDate}_${cleanAmount}`;\n\n  results.push({\n    json: {\n      ...json,\n      clean_date: cleanDate,\n      clean_amount: cleanAmount,\n      match_key: matchKey,\n      sumber: 'Bank'\n    }\n  });\n}\n\nreturn results;\n"
      },
      "type": "n8n-nodes-base.code",
      "typeVersion": 2,
      "position": [
        608,
        144
      ],
      "id": "3260668a-3a7a-419c-ae90-95e04fecc368",
      "name": "clean bank data"
    },
    {
      "parameters": {},
      "type": "n8n-nodes-base.merge",
      "typeVersion": 3.2,
      "position": [
        784,
        16
      ],
      "id": "d463c629-2958-42f4-999e-0035f610ed0f",
      "name": "Merge"
    },
    {
      "parameters": {
        "jsCode": "// CODE NODE: ANALISA REKONSILIASI LENGKAP (tanpa Union)\nconst items = $input.all();\nconst grouped = {};\n\n// 1. Group by match_key\nfor (const item of items) {\n  const key = item.json.match_key;\n  if (!grouped[key]) {\n    grouped[key] = { sources: [], details: [] };\n  }\n  grouped[key].sources.push(item.json.sumber);\n  grouped[key].details.push(item.json);\n}\n\n// 2. Bangun hasil analisa\nconst results = [];\nfor (const [key, group] of Object.entries(grouped)) {\n  const hasInternal = group.sources.includes('Internal');\n  const hasBank = group.sources.includes('Bank');\n\n  let status, pesan, priority;\n  if (hasInternal && hasBank) {\n    status = 'MATCHED';\n    pesan = '✅ Data klop (Cocok).';\n    priority = 'Low';\n  } else if (hasInternal && !hasBank) {\n    status = 'MISSING IN BANK';\n    pesan = '⚠️ Tercatat di Internal, tapi tidak ada di Bank.';\n    priority = 'High';\n  } else if (!hasInternal && hasBank) {\n    status = 'UNRECORDED INTERNAL';\n    pesan = '⚠️ Ada di Bank, tapi tidak tercatat di Internal.';\n    priority = 'Medium';\n  }\n\n  const internal = group.details.find(d => d.sumber === 'Internal');\n  const bank = group.details.find(d => d.sumber === 'Bank');\n  const refDate = (internal || bank)?.clean_date;\n  const amount = (internal || bank)?.clean_amount;\n\n  results.push({\n    json: {\n      Tanggal: refDate,\n      Nominal: amount,\n      Status: status,\n      Pesan: pesan,\n      Prioritas: priority,\n      Internal_ID: internal?.['ID Referensi'] || 'N/A',\n      Bank_ID: bank?.['ID Transaksi Bank'] || 'N/A',\n      Deskripsi: internal?.Deskripsi || bank?.['Deskripsi Transaksi'] || '-',\n      Match_Key: key,\n      Sources: group.sources.join(' + ')\n    }\n  });\n}\n\nreturn results;"
      },
      "type": "n8n-nodes-base.code",
      "typeVersion": 2,
      "position": [
        976,
        16
      ],
      "id": "78daaec0-6d2f-44f1-8d5b-4ccd3ddb2e11",
      "name": "analisis status"
    },
    {
      "parameters": {
        "conditions": {
          "options": {
            "caseSensitive": true,
            "leftValue": "",
            "typeValidation": "strict",
            "version": 3
          },
          "conditions": [
            {
              "id": "2acf7717-0654-4b8b-903a-c2ebaa65ec71",
              "leftValue": "={{ $json.status }}",
              "rightValue": "MATCHED",
              "operator": {
                "type": "string",
                "operation": "equals",
                "name": "filter.operator.equals"
              }
            }
          ],
          "combinator": "and"
        },
        "options": {}
      },
      "type": "n8n-nodes-base.if",
      "typeVersion": 2.3,
      "position": [
        1184,
        16
      ],
      "id": "d1058cbd-78b8-4494-a053-f16ab97130b3",
      "name": "cek status match"
    },
    {
      "parameters": {
        "unit": "minutes"
      },
      "type": "n8n-nodes-base.wait",
      "typeVersion": 1.1,
      "position": [
        1392,
        112
      ],
      "id": "1a204f77-85e9-4769-947b-7fee593361e8",
      "name": "Wait",
      "webhookId": "bbf62a26-bc55-4b87-9a97-5b0df82c1449"
    },
    {
      "parameters": {
        "chatId": "1535237765",
        "text": "=🚨 **LAPORAN SELISIH KEUANGAN**  📅 Tanggal: {{ $json.Tanggal }} 💰 Nominal: Rp {{ $json.Nominal }}  ⚠️ **Status: {{ $json.Status }}** 📝 Ket: {{ $json.Pesan }}  🔍 Ref Internal: {{ $json.Internal_ID }} 🏦 Ref Bank: {{ $json.Bank_ID }} ℹ️ Desc: {{ $json.Deskripsi }}",
        "additionalFields": {}
      },
      "type": "n8n-nodes-base.telegram",
      "typeVersion": 1.2,
      "position": [
        1392,
        -80
      ],
      "id": "fae2357e-9627-40ab-916c-b33d6e2a6747",
      "name": "kirim laporan data cocok",
      "webhookId": "42c8f6a5-b7ea-4d95-8c75-36d30e87dc57",
      "credentials": {
        "telegramApi": {
          "id": "UeW4rIKFaGuH61DK",
          "name": "bot renjeun"
        }
      }
    },
    {
      "parameters": {
        "chatId": "1535237765",
        "text": "=🚨 **LAPORAN SELISIH KEUANGAN**  📅 Tanggal: {{ $json.Tanggal }} 💰 Nominal: Rp {{ $json.Nominal }}  ⚠️ **Status: {{ $json.Status }}** 📝 Ket: {{ $json.Pesan }}  🔍 Ref Internal: {{ $json.Internal_ID }} 🏦 Ref Bank: {{ $json.Bank_ID }} ℹ️ Desc: {{ $json.Deskripsi }}",
        "additionalFields": {}
      },
      "type": "n8n-nodes-base.telegram",
      "typeVersion": 1.2,
      "position": [
        1600,
        112
      ],
      "id": "1e483597-69bd-4787-8bb8-630b1e6ea5fe",
      "name": "Send a text message",
      "webhookId": "07a846aa-f919-4c4f-a9a8-5457b120f176",
      "credentials": {
        "telegramApi": {
          "id": "n7cxOzcieENzevJa",
          "name": "Telegram account 2"
        }
      }
    }
  ],
  "connections": {
    "Schedule Trigger": {
      "main": [
        [
          {
            "node": "data internal",
            "type": "main",
            "index": 0
          },
          {
            "node": "data bank",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "data internal": {
      "main": [
        [
          {
            "node": "filter baris",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "data bank": {
      "main": [
        [
          {
            "node": "Extract from File",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Extract from File": {
      "main": [
        [
          {
            "node": "clean bank data",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "filter baris": {
      "main": [
        [
          {
            "node": "Merge",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "clean bank data": {
      "main": [
        [
          {
            "node": "Merge",
            "type": "main",
            "index": 1
          }
        ]
      ]
    },
    "Merge": {
      "main": [
        [
          {
            "node": "analisis status",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "analisis status": {
      "main": [
        [
          {
            "node": "cek status match",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "cek status match": {
      "main": [
        [
          {
            "node": "kirim laporan data cocok",
            "type": "main",
            "index": 0
          }
        ],
        [
          {
            "node": "Wait",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Wait": {
      "main": [
        [
          {
            "node": "Send a text message",
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
