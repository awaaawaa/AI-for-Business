{
  "nodes": [
    {
      "parameters": {
        "updates": [
          "message"
        ],
        "additionalFields": {}
      },
      "type": "n8n-nodes-base.telegramTrigger",
      "typeVersion": 1.2,
      "position": [
        0,
        0
      ],
      "id": "1c7c0911-7129-4624-b76b-5975eeba55bf",
      "name": "Telegram Trigger",
      "webhookId": "e707f301-b0c7-4f87-a9b2-809c4202ca67",
      "credentials": {
        "telegramApi": {
          "id": "wFhaxulSc1T2JgPT",
          "name": "Telegram account 3"
        }
      }
    },
    {
      "parameters": {
        "promptType": "define",
        "text": "={{ $json.message.text }}",
        "options": {
          "systemMessage": "Saya adalah seorang Logic Architect, seorang perancang pola utama yang mendedikasikan diri untuk dunia proyek kerajinan tangan, khususnya yang berbahan kain flanel. Peran saya bukan sekadar menjawab pertanyaan, melainkan menjadi navigator bagi pengguna untuk menyusun ide, merangkai masalah yang berantakan, dan memetakan langkah-langkah produksi agar semuanya menjadi terstruktur dan efisien. Saya percaya bahwa setiap tantangan adalah seperti gumpalan flanel yang belum terbentuk, dan tugas saya adalah membantu pengguna membangun logika di baliknya sehingga menjadi sebuah karya yang indah dan bernilai tinggi.  Jika pengguna bertanya tentang produk, carilah kata kunci yang paling mendekati di Google Sheets. Jangan menyerah jika kata katanya tidak persis sama, coba cari bagian dari kata tersebut."
        }
      },
      "type": "@n8n/n8n-nodes-langchain.agent",
      "typeVersion": 3.1,
      "position": [
        208,
        0
      ],
      "id": "dca7b9c9-bc89-4dec-b725-4ad8990f0511",
      "name": "AI Agent"
    },
    {
      "parameters": {
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.lmChatGoogleGemini",
      "typeVersion": 1,
      "position": [
        224,
        160
      ],
      "id": "90a019b8-eacb-4905-b598-a13fcf0059df",
      "name": "Google Gemini Chat Model",
      "credentials": {
        "googlePalmApi": {
          "id": "qA1uVlz3z2Seif8h",
          "name": "Google Gemini(PaLM) Api account 3"
        }
      }
    },
    {
      "parameters": {
        "chatId": "={{ $('Telegram Trigger').item.json.message.chat.id }}",
        "text": "={{ $json.output }}",
        "additionalFields": {
          "appendAttribution": false,
          "parse_mode": "HTML"
        }
      },
      "type": "n8n-nodes-base.telegram",
      "typeVersion": 1.2,
      "position": [
        560,
        0
      ],
      "id": "4364a210-4f42-4737-8d42-d023b8440f08",
      "name": "Send a text message",
      "webhookId": "6d1c9d49-026c-47ef-ab17-35cdc2a9ce38",
      "credentials": {
        "telegramApi": {
          "id": "wFhaxulSc1T2JgPT",
          "name": "Telegram account 3"
        }
      }
    },
    {
      "parameters": {
        "documentId": {
          "__rl": true,
          "value": "11YD-wpY-ZjyQU4EZkQYNR-iWWG_2o72DoVCY6omntKU",
          "mode": "list",
          "cachedResultName": "tabel harga kerajinan tangan",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/11YD-wpY-ZjyQU4EZkQYNR-iWWG_2o72DoVCY6omntKU/edit?usp=drivesdk"
        },
        "sheetName": {
          "__rl": true,
          "value": "gid=0",
          "mode": "list",
          "cachedResultName": "Sheet1",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/11YD-wpY-ZjyQU4EZkQYNR-iWWG_2o72DoVCY6omntKU/edit#gid=0"
        },
        "options": {}
      },
      "type": "n8n-nodes-base.googleSheetsTool",
      "typeVersion": 4.7,
      "position": [
        416,
        176
      ],
      "id": "2b852ace-d087-4e8b-bc8b-f5d0add3cd47",
      "name": "Get row(s) in sheet in Google Sheets",
      "credentials": {
        "googleSheetsOAuth2Api": {
          "id": "0ytqo2ykBUkIcQvW",
          "name": "Google Sheets account"
        }
      }
    }
  ],
  "connections": {
    "Telegram Trigger": {
      "main": [
        [
          {
            "node": "AI Agent",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "AI Agent": {
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
    "Google Gemini Chat Model": {
      "ai_languageModel": [
        [
          {
            "node": "AI Agent",
            "type": "ai_languageModel",
            "index": 0
          }
        ]
      ]
    },
    "Get row(s) in sheet in Google Sheets": {
      "ai_tool": [
        [
          {
            "node": "AI Agent",
            "type": "ai_tool",
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
