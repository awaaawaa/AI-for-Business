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
      "id": "ef1d8dee-05b9-4d38-a4ea-76b5da3bc539",
      "name": "Telegram Trigger",
      "webhookId": "aad1200d-342c-4d6f-a216-7c606409b8a1",
      "credentials": {
        "telegramApi": {
          "id": "UeW4rIKFaGuH61DK",
          "name": "bot renjeun"
        }
      }
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
              "id": "7410c3e1-147c-4100-b20f-40f0b6d7b356",
              "leftValue": "={{ $json.message.text }}",
              "rightValue": "Bagaimana prosedur reimbursement",
              "operator": {
                "type": "string",
                "operation": "contains"
              }
            },
            {
              "id": "133e82b2-3260-42ae-8e80-a35b82d6c0b5",
              "leftValue": "={{ $json.message.text }}",
              "rightValue": "Prosedur pengajuan cuti tahunan",
              "operator": {
                "type": "string",
                "operation": "contains"
              }
            },
            {
              "id": "ae3caad9-25d5-4f27-92b8-ebf027316b7d",
              "leftValue": "={{ $json.message.text }}",
              "rightValue": "Bagaimana aturan lembur di perusahaan?",
              "operator": {
                "type": "string",
                "operation": "contains"
              }
            },
            {
              "id": "d0dc7553-8013-4c96-8a1b-92ab45138345",
              "leftValue": "={{ $json.message.text }}",
              "rightValue": "Apa syarat klaim asuransi kesehatan?",
              "operator": {
                "type": "string",
                "operation": "contains"
              }
            },
            {
              "id": "0e7514d3-5562-4e8a-b1be-3c64b26ab701",
              "leftValue": "={{ $json.message.text }}",
              "rightValue": "Bagaimana prosedur permintaan alat kerja baru?",
              "operator": {
                "type": "string",
                "operation": "contains"
              }
            },
            {
              "id": "9fbec772-166c-4405-9c16-46befa4f2e6c",
              "leftValue": "={{ $json.message.text }}",
              "rightValue": "1. Bagaimana prosedur reimbursement?",
              "operator": {
                "type": "string",
                "operation": "contains"
              }
            },
            {
              "id": "e878d8d7-c769-430f-bedb-ee2726c82488",
              "leftValue": "={{ $json.message.text }}",
              "rightValue": "2. Prosedur pengajuan cuti tahunan",
              "operator": {
                "type": "string",
                "operation": "contains"
              }
            },
            {
              "id": "09939844-7a7b-4580-9a8a-a932f0b272e3",
              "leftValue": "={{ $json.message.text }}",
              "rightValue": "3. Bagimana aturan lembur di perusahaan?",
              "operator": {
                "type": "string",
                "operation": "contains"
              }
            },
            {
              "id": "12c930fb-64e6-4bd9-a5b3-9c6c9f6265a8",
              "leftValue": "={{ $json.message.text }}",
              "rightValue": "4. Apa syarat klaim asuransi kesehatan?",
              "operator": {
                "type": "string",
                "operation": "contains"
              }
            },
            {
              "id": "fddc6f54-0ac2-452f-97b5-83bb6a934612",
              "leftValue": "={{ $json.message.text }}",
              "rightValue": "5. Bagaimana prosedur permintaan alat kerja baru?",
              "operator": {
                "type": "string",
                "operation": "contains"
              }
            }
          ],
          "combinator": "or"
        },
        "options": {}
      },
      "type": "n8n-nodes-base.if",
      "typeVersion": 2.3,
      "position": [
        208,
        0
      ],
      "id": "7a1e38de-f2a8-421e-9119-d8f8439dedac",
      "name": "Memastikan sesuai format"
    },
    {
      "parameters": {
        "chatId": "1535237765",
        "text": "=Pertanyaan yang Anda kirimkan tidak sesuai, harap gunakan pertanyaan dibawah ini:  \n1. Bagaimana prosedur reimbursement?  \n2. Prosedur pengajuan cuti tahunan  \n3. Bagaimana aturan lembur di perusahaan?  \n4. Apa syarat klaim asuransi kesehatan?  \n5. Bagaimana prosedur permintaan alat kerja baru?",
        "additionalFields": {}
      },
      "type": "n8n-nodes-base.telegram",
      "typeVersion": 1.2,
      "position": [
        352,
        144
      ],
      "id": "54c11216-254c-41f8-8174-e7b3db58f22a",
      "name": "False Output",
      "webhookId": "f55158f7-6d89-4e5d-9987-58e234f28df2",
      "credentials": {
        "telegramApi": {
          "id": "UeW4rIKFaGuH61DK",
          "name": "bot renjeun"
        }
      }
    },
    {
      "parameters": {
        "promptType": "define",
        "text": "=Anda adalah SOP AI Agent.\n\nATURAN KERAS:\n\nAnda WAJIB menggunakan TOOL \"Data Pertanyaan\" sebelum menjawab.\n\nJawaban HARUS diambil dari hasil tool.\n\nDILARANG menggunakan pengetahuan umum.\n\nJika data tidak ditemukan, jawab: \"Maaf, informasi tersebut tidak tersedia di SOP.\"\n\nPertanyaan pengguna:\n{{ $node[\"Telegram Trigger\"].json.message.text }}\n\nJawaban berdasarkan SOP:",
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.agent",
      "typeVersion": 3.1,
      "position": [
        608,
        -16
      ],
      "id": "d02846bf-ffb2-4dfc-a77f-b5e32eaeec07",
      "name": "AI Agent"
    },
    {
      "parameters": {
        "model": "openai/gpt-oss-120b",
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.lmChatGroq",
      "typeVersion": 1,
      "position": [
        608,
        192
      ],
      "id": "93ffe934-eb62-4209-9c30-1ed6d91be0dc",
      "name": "Groq Chat Model",
      "credentials": {
        "groqApi": {
          "id": "pDEFMHXiNQAKuWD5",
          "name": "renjun"
        }
      }
    },
    {
      "parameters": {
        "documentId": {
          "__rl": true,
          "value": "1EU3Suq52DPvar-vjeggZphfoGXf5wEGfL4LGZPKHyyE",
          "mode": "list",
          "cachedResultName": "Copy of Data Pertanyaan untuk Karyawan",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1EU3Suq52DPvar-vjeggZphfoGXf5wEGfL4LGZPKHyyE/edit?usp=drivesdk"
        },
        "sheetName": {
          "__rl": true,
          "value": "gid=0",
          "mode": "list",
          "cachedResultName": "Sheet1",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1EU3Suq52DPvar-vjeggZphfoGXf5wEGfL4LGZPKHyyE/edit#gid=0"
        },
        "options": {}
      },
      "type": "n8n-nodes-base.googleSheetsTool",
      "typeVersion": 4.7,
      "position": [
        768,
        192
      ],
      "id": "93093266-a624-4d4a-9126-e780f5b8f8ed",
      "name": "Get row(s) in sheet in Google Sheets",
      "credentials": {
        "googleSheetsOAuth2Api": {
          "id": "1i4CpejrRiWAa25G",
          "name": "Google Sheets account 3"
        }
      }
    },
    {
      "parameters": {
        "chatId": "1535237765",
        "text": "={{ $json.output }}",
        "additionalFields": {}
      },
      "type": "n8n-nodes-base.telegram",
      "typeVersion": 1.2,
      "position": [
        960,
        -16
      ],
      "id": "70d9ec63-73d2-4864-8489-a84ec0d2fc2b",
      "name": "True Output",
      "webhookId": "79637ff2-8c1a-4d4a-88b8-f2d2df430b10",
      "credentials": {
        "telegramApi": {
          "id": "UeW4rIKFaGuH61DK",
          "name": "bot renjeun"
        }
      }
    }
  ],
  "connections": {
    "Telegram Trigger": {
      "main": [
        [
          {
            "node": "Memastikan sesuai format",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Memastikan sesuai format": {
      "main": [
        [
          {
            "node": "AI Agent",
            "type": "main",
            "index": 0
          }
        ],
        [
          {
            "node": "False Output",
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
            "node": "True Output",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Groq Chat Model": {
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
