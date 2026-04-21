{
  "nodes": [
    {
      "parameters": {
        "rule": {
          "interval": [
            {
              "triggerAtHour": 7
            }
          ]
        }
      },
      "type": "n8n-nodes-base.scheduleTrigger",
      "typeVersion": 1.3,
      "position": [
        -80,
        32
      ],
      "id": "f9977dc3-d56c-4283-9148-75a299f6e075",
      "name": "Schedule Trigger"
    },
    {
      "parameters": {
        "url": "https://www.cnbcindonesia.com/market/rss",
        "options": {}
      },
      "type": "n8n-nodes-base.rssFeedRead",
      "typeVersion": 1.2,
      "position": [
        208,
        -96
      ],
      "id": "1ecc3878-38b1-4fa5-8469-9386c5510671",
      "name": "CNBC Indonesia RSS"
    },
    {
      "parameters": {
        "url": "https://finance.detik.com/rss",
        "options": {}
      },
      "type": "n8n-nodes-base.rssFeedRead",
      "typeVersion": 1.2,
      "position": [
        208,
        32
      ],
      "id": "5d2729ff-2d6a-4fe6-bbc1-6455c8dcffbd",
      "name": "Finance Detik RSS"
    },
    {
      "parameters": {},
      "type": "n8n-nodes-base.merge",
      "typeVersion": 3.2,
      "position": [
        480,
        16
      ],
      "id": "8ae0ca20-b3b0-4fdb-a6c7-40b944f5f9b6",
      "name": "Merge"
    },
    {
      "parameters": {
        "maxItems": 5
      },
      "type": "n8n-nodes-base.limit",
      "typeVersion": 1,
      "position": [
        688,
        16
      ],
      "id": "b52d1463-1c15-4c9e-8cb3-98a16f7d5f1e",
      "name": "Limit"
    },
    {
      "parameters": {
        "url": "={{ $json.link }}",
        "options": {}
      },
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 4.4,
      "position": [
        896,
        16
      ],
      "id": "8a8af8e1-2045-469f-9d9f-480c3ebe19db",
      "name": "unduh halaman we dari setiap url"
    },
    {
      "parameters": {
        "operation": "extractHtmlContent",
        "extractionValues": {
          "values": [
            {
              "key": "text",
              "cssSelector": "body"
            }
          ]
        },
        "options": {}
      },
      "type": "n8n-nodes-base.html",
      "typeVersion": 1.2,
      "position": [
        -32,
        256
      ],
      "id": "2fa64ed1-a1dd-44ca-907c-fb331e0fb762",
      "name": "HTML"
    },
    {
      "parameters": {
        "fieldsToAggregate": {
          "fieldToAggregate": [
            {
              "fieldToAggregate": "text"
            }
          ]
        },
        "options": {}
      },
      "type": "n8n-nodes-base.aggregate",
      "typeVersion": 1,
      "position": [
        176,
        256
      ],
      "id": "e87441c7-12e0-4d31-a3c0-2011abeec054",
      "name": "menggabungkan menjadi 1 blok teks besar"
    },
    {
      "parameters": {
        "chatId": "1535237765",
        "text": "={{ $json.text }}",
        "additionalFields": {
          "parse_mode": "Markdown"
        }
      },
      "type": "n8n-nodes-base.telegram",
      "typeVersion": 1.2,
      "position": [
        704,
        256
      ],
      "id": "baa2a416-4875-44be-9f03-ac7c49d41c51",
      "name": "Send a text message",
      "webhookId": "eeafcb0c-daa1-4ec3-b2ff-85c9337c7a59",
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
        "text": "=Tolong rangkum berita-berita berikut ini menjadi poin-poin yang singkat dan informatif:\n\n{{ $json.text }}",
        "batching": {}
      },
      "type": "@n8n/n8n-nodes-langchain.chainLlm",
      "typeVersion": 1.9,
      "position": [
        368,
        256
      ],
      "id": "3674005c-b48f-4860-a226-a6ad460ee773",
      "name": "Basic LLM Chain"
    },
    {
      "parameters": {
        "model": "openai/gpt-oss-120b:free",
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.lmChatOpenRouter",
      "typeVersion": 1,
      "position": [
        304,
        464
      ],
      "id": "417eca2f-b820-42e1-8738-48b30f4bbea4",
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
    "Schedule Trigger": {
      "main": [
        [
          {
            "node": "CNBC Indonesia RSS",
            "type": "main",
            "index": 0
          },
          {
            "node": "Finance Detik RSS",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "CNBC Indonesia RSS": {
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
    "Finance Detik RSS": {
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
            "node": "Limit",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Limit": {
      "main": [
        [
          {
            "node": "unduh halaman we dari setiap url",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "unduh halaman we dari setiap url": {
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
            "node": "menggabungkan menjadi 1 blok teks besar",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "menggabungkan menjadi 1 blok teks besar": {
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
            "node": "Send a text message",
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
