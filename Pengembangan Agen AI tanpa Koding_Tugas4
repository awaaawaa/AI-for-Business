{
  "nodes": [
    {
      "parameters": {},
      "type": "n8n-nodes-base.manualTrigger",
      "typeVersion": 1,
      "position": [
        0,
        0
      ],
      "id": "0baca7e6-5fe4-42eb-a336-f350283111a5",
      "name": "When clicking ‘Execute workflow’"
    },
    {
      "parameters": {
        "operation": "download",
        "fileId": {
          "__rl": true,
          "value": "1he5idmRUhjT0IrYdw_LXEflkIavdO0CU",
          "mode": "list",
          "cachedResultName": "Panduan Penulisan Ilmiah Tugas Akhir Skripsi.pdf",
          "cachedResultUrl": "https://drive.google.com/file/d/1he5idmRUhjT0IrYdw_LXEflkIavdO0CU/view?usp=drivesdk"
        },
        "options": {}
      },
      "type": "n8n-nodes-base.googleDrive",
      "typeVersion": 3,
      "position": [
        208,
        0
      ],
      "id": "022c05fb-8e12-4f0b-a175-3e58eef9493b",
      "name": "Download file",
      "credentials": {
        "googleDriveOAuth2Api": {
          "id": "m0LVenic0HhXrhGT",
          "name": "Google Drive account"
        }
      }
    },
    {
      "parameters": {
        "mode": "insert",
        "tableName": {
          "__rl": true,
          "value": "document",
          "mode": "list",
          "cachedResultName": "document"
        },
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.vectorStoreSupabase",
      "typeVersion": 1.3,
      "position": [
        416,
        0
      ],
      "id": "a3a60f64-7e10-482d-9abe-3b5b91e7da12",
      "name": "Supabase Vector Store",
      "credentials": {
        "supabaseApi": {
          "id": "GiCwtEdPUmu304eG",
          "name": "Supabase account"
        }
      }
    },
    {
      "parameters": {
        "dataType": "binary",
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.documentDefaultDataLoader",
      "typeVersion": 1.1,
      "position": [
        560,
        208
      ],
      "id": "79dc319b-3b2f-4bb7-acae-f90f36bdeb44",
      "name": "Default Data Loader"
    },
    {
      "parameters": {
        "modelName": "models/gemini-embedding-2-preview"
      },
      "type": "@n8n/n8n-nodes-langchain.embeddingsGoogleGemini",
      "typeVersion": 1,
      "position": [
        464,
        208
      ],
      "id": "d68ea318-b79f-4cae-a3ea-4548b70707be",
      "name": "Embeddings Google Gemini",
      "credentials": {
        "googlePalmApi": {
          "id": "qA1uVlz3z2Seif8h",
          "name": "Google Gemini(PaLM) Api account 3"
        }
      }
    },
    {
      "parameters": {
        "public": true,
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.chatTrigger",
      "typeVersion": 1.4,
      "position": [
        16,
        448
      ],
      "id": "baaa31ad-2317-459f-9635-5c8da2dd61a0",
      "name": "When chat message received",
      "webhookId": "6767faa5-8d96-45ae-b17e-3093e209efae"
    },
    {
      "parameters": {
        "options": {
          "systemMessage": "Kamu asisten yang membantu penulisan ilmiah untuk tugas \nakhir (TA). Gunakan tool Supabase Vector Store untuk \nmemberikan bantuan. \nJika informasi tidak tersedia dalam database yang disediakan, \njangan menjawab dengan mengarang sendiri, tetapi berikan \njawaban “Maaf, saya belum dapat menjawab karena saya \ntemukan dalam informasi yang tersedia.”"
        }
      },
      "type": "@n8n/n8n-nodes-langchain.agent",
      "typeVersion": 3.1,
      "position": [
        224,
        448
      ],
      "id": "cfc09f6b-ef14-4eed-ba9e-5a5c1f38c4ed",
      "name": "AI Agent"
    },
    {
      "parameters": {
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.lmChatGoogleGemini",
      "typeVersion": 1,
      "position": [
        96,
        656
      ],
      "id": "2b67b9dc-cfb3-4c20-9b89-edae9ff74cff",
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
        "mode": "retrieve-as-tool",
        "toolDescription": "Pangil Tool Supabase Vector Store ini untuk mendapatkan informasi panduan menulis bab 1 tulisan ilmiah",
        "tableName": {
          "__rl": true,
          "value": "document",
          "mode": "list",
          "cachedResultName": "document"
        },
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.vectorStoreSupabase",
      "typeVersion": 1.3,
      "position": [
        576,
        448
      ],
      "id": "881bda3f-5537-4b58-a144-83ababf93d0d",
      "name": "Supabase Vector Store1",
      "credentials": {
        "supabaseApi": {
          "id": "GiCwtEdPUmu304eG",
          "name": "Supabase account"
        }
      }
    },
    {
      "parameters": {},
      "type": "@n8n/n8n-nodes-langchain.memoryPostgresChat",
      "typeVersion": 1.3,
      "position": [
        240,
        656
      ],
      "id": "b00c7b3e-2ace-4094-ae92-7bc4308ab881",
      "name": "Postgres Chat Memory",
      "credentials": {
        "postgres": {
          "id": "NYDHxWJ9iB7cFcAB",
          "name": "Postgres account"
        }
      }
    }
  ],
  "connections": {
    "When clicking ‘Execute workflow’": {
      "main": [
        [
          {
            "node": "Download file",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Download file": {
      "main": [
        [
          {
            "node": "Supabase Vector Store",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Default Data Loader": {
      "ai_document": [
        [
          {
            "node": "Supabase Vector Store",
            "type": "ai_document",
            "index": 0
          }
        ]
      ]
    },
    "Embeddings Google Gemini": {
      "ai_embedding": [
        [
          {
            "node": "Supabase Vector Store",
            "type": "ai_embedding",
            "index": 0
          },
          {
            "node": "Supabase Vector Store1",
            "type": "ai_embedding",
            "index": 0
          }
        ]
      ]
    },
    "When chat message received": {
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
    "Supabase Vector Store1": {
      "ai_tool": [
        [
          {
            "node": "AI Agent",
            "type": "ai_tool",
            "index": 0
          }
        ]
      ]
    },
    "Postgres Chat Memory": {
      "ai_memory": [
        [
          {
            "node": "AI Agent",
            "type": "ai_memory",
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
