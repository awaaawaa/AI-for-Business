{
  "nodes": [
    {
      "parameters": {
        "rule": {
          "interval": [
            {
              "field": "weeks",
              "triggerAtHour": 7
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
      "id": "479ef934-83ed-4435-9615-4679e4ac7052",
      "name": "setiap hari minggu"
    },
    {
      "parameters": {
        "documentId": {
          "__rl": true,
          "value": "1H2UUBfefkbugozfYa4gwaa8pKP1oZqYr1mDtKAnYtho",
          "mode": "list",
          "cachedResultName": "Copy of Data Dummy Catatan Keuangan",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1H2UUBfefkbugozfYa4gwaa8pKP1oZqYr1mDtKAnYtho/edit?usp=drivesdk"
        },
        "sheetName": {
          "__rl": true,
          "value": "gid=0",
          "mode": "list",
          "cachedResultName": "Sheet1",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1H2UUBfefkbugozfYa4gwaa8pKP1oZqYr1mDtKAnYtho/edit#gid=0"
        },
        "options": {}
      },
      "type": "n8n-nodes-base.googleSheets",
      "typeVersion": 4.7,
      "position": [
        208,
        0
      ],
      "id": "2daa80df-4f0b-4e80-bac0-12aef28a1a90",
      "name": "ambil log pengeluaran",
      "credentials": {
        "googleSheetsOAuth2Api": {
          "id": "1i4CpejrRiWAa25G",
          "name": "Google Sheets account 3"
        }
      }
    },
    {
      "parameters": {
        "jsCode": "const items = $input.all();\nconst today = new Date();\ntoday.setHours(23, 59, 59, 999); // inklusif hari ini sampai akhir hari\n\nconst sevenDaysAgo = new Date();\nsevenDaysAgo.setDate(today.getDate() - 7);\nsevenDaysAgo.setHours(0, 0, 0, 0);\n\nlet weeklyExpenses = [];\nlet formattedString = \"Data pengeluaran saya minggu ini:\\n\";\nlet hasExpenses = false;\n\nfor (const item of items) {\n  const rawTanggal = item.json.Tanggal; // format: \"13/04/2026\"\n  \n  // Parse manual DD/MM/YYYY → YYYY-MM-DD agar valid di semua engine\n  const [day, month, year] = rawTanggal.split(\"/\");\n  const expenseDate = new Date(`${year}-${month}-${day}`);\n\n  if (expenseDate >= sevenDaysAgo && expenseDate <= today) {\n    weeklyExpenses.push(item.json);\n    formattedString += `- ${item.json.Deskripsi}: Rp${item.json[\"Jumlah (IDR)\"]}\\n`;\n    hasExpenses = true;\n  }\n}\n\nreturn [{\n  json: {\n    promptData: formattedString,\n    hasExpenses: hasExpenses\n  }\n}];\n"
      },
      "type": "n8n-nodes-base.code",
      "typeVersion": 2,
      "position": [
        416,
        0
      ],
      "id": "ac0be664-2851-429f-9ed2-a7f2bd2e1a60",
      "name": "Filter 7 hari dan format text"
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
              "id": "d3e9ef8c-84c7-43f8-90ad-068fa3f5ac6d",
              "leftValue": "={{ $json.hasExpenses }}",
              "rightValue": "",
              "operator": {
                "type": "boolean",
                "operation": "true",
                "singleValue": true
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
        624,
        0
      ],
      "id": "3e6c32a7-4efd-46db-a2b0-b7d6c820161c",
      "name": "If"
    },
    {
      "parameters": {
        "promptType": "define",
        "text": "={{ $node[\"Filter 7 hari dan format text\"].json.promptData }}\n\n---\nInstruksi: \"Tulis ringkasan kebiasaan belanja saya minggu ini dan beri 1 saran penghematan.\"",
        "batching": {}
      },
      "type": "@n8n/n8n-nodes-langchain.chainLlm",
      "typeVersion": 1.9,
      "position": [
        832,
        -96
      ],
      "id": "090941c5-43f9-4195-832a-f12fb131643a",
      "name": "analisis"
    },
    {
      "parameters": {
        "model": "openai/gpt-oss-120b:free",
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.lmChatOpenRouter",
      "typeVersion": 1,
      "position": [
        960,
        -208
      ],
      "id": "3c84fe1b-e2aa-4116-8885-69a9cf048cfe",
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
        "chatId": "1535237765",
        "text": "={{ $json.text }}",
        "additionalFields": {}
      },
      "type": "n8n-nodes-base.telegram",
      "typeVersion": 1.2,
      "position": [
        1184,
        -96
      ],
      "id": "f1636d91-8286-4eb0-b0df-326b75056728",
      "name": "pesan true",
      "webhookId": "3fe5197e-39f2-42d3-918c-f8016f91484e",
      "credentials": {
        "telegramApi": {
          "id": "n7cxOzcieENzevJa",
          "name": "mark lee"
        }
      }
    },
    {
      "parameters": {
        "chatId": "1535237765",
        "text": "Tidak ditemukan log pengeluaran untuk 7 hari terakhir.",
        "additionalFields": {}
      },
      "type": "n8n-nodes-base.telegram",
      "typeVersion": 1.2,
      "position": [
        880,
        144
      ],
      "id": "e02c8ffb-92a0-44e6-8bd3-cf44906cfdae",
      "name": "pesan false",
      "webhookId": "37ccd6b6-81d3-45a2-90cd-7f769846254d",
      "credentials": {
        "telegramApi": {
          "id": "n7cxOzcieENzevJa",
          "name": "mark lee"
        }
      }
    }
  ],
  "connections": {
    "setiap hari minggu": {
      "main": [
        [
          {
            "node": "ambil log pengeluaran",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "ambil log pengeluaran": {
      "main": [
        [
          {
            "node": "Filter 7 hari dan format text",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Filter 7 hari dan format text": {
      "main": [
        [
          {
            "node": "If",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "If": {
      "main": [
        [
          {
            "node": "analisis",
            "type": "main",
            "index": 0
          }
        ],
        [
          {
            "node": "pesan false",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "analisis": {
      "main": [
        [
          {
            "node": "pesan true",
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
            "node": "analisis",
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
