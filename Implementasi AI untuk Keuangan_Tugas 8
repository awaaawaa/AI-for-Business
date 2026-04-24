{
  "nodes": [
    {
      "parameters": {
        "rule": {
          "interval": [
            {
              "field": "minutes",
              "minutesInterval": 15
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
      "id": "14800546-3de4-4f89-b14e-b1db1a246441",
      "name": "tiap 15 menit"
    },
    {
      "parameters": {
        "promptType": "define",
        "text": "Analyze the sentiment of the following tweet. Respond ONLY with ONE word: 'Positive', 'Negative', or 'Neutral'.\n\nTweet:\n{{ $json.text }}\n",
        "batching": {}
      },
      "type": "@n8n/n8n-nodes-langchain.chainLlm",
      "typeVersion": 1.9,
      "position": [
        416,
        0
      ],
      "id": "b1239694-2b08-408e-b3d3-af829ba945c1",
      "name": "analisis sentimen"
    },
    {
      "parameters": {
        "model": "liquid/lfm-2.5-1.2b-instruct:free",
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.lmChatOpenRouter",
      "typeVersion": 1,
      "position": [
        352,
        208
      ],
      "id": "ed986b25-a7e8-451f-be85-c8d56944eed8",
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
        "operation": "append",
        "documentId": {
          "__rl": true,
          "value": "1Lma1X-KY3cEMbCLJEKKEChgYMPlppMGNTBb5LwWnyyg",
          "mode": "list",
          "cachedResultName": "$BTC OR $ETH Sentimen Media Sosial",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1Lma1X-KY3cEMbCLJEKKEChgYMPlppMGNTBb5LwWnyyg/edit?usp=drivesdk"
        },
        "sheetName": {
          "__rl": true,
          "value": "gid=0",
          "mode": "list",
          "cachedResultName": "Data Mentah",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1Lma1X-KY3cEMbCLJEKKEChgYMPlppMGNTBb5LwWnyyg/edit#gid=0"
        },
        "columns": {
          "mappingMode": "defineBelow",
          "value": {
            "Timestamp": "={{ $now.toFormat(\"yyyy-MM-dd HH:mm:ss\") }}",
            "Sentimen": "={{ $json.text }}"
          },
          "matchingColumns": [],
          "schema": [
            {
              "id": "Timestamp",
              "displayName": "Timestamp",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "Sentimen",
              "displayName": "Sentimen",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            }
          ],
          "attemptToConvertTypes": false,
          "convertFieldsToString": false
        },
        "options": {}
      },
      "type": "n8n-nodes-base.googleSheets",
      "typeVersion": 4.7,
      "position": [
        752,
        0
      ],
      "id": "9442d309-5df0-47a1-aebe-2219a37cb6e9",
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
        0,
        384
      ],
      "id": "d7756e29-7d28-415f-9ccf-f11f6f35dd50",
      "name": "tiap jam 7 pagi"
    },
    {
      "parameters": {
        "documentId": {
          "__rl": true,
          "value": "1Lma1X-KY3cEMbCLJEKKEChgYMPlppMGNTBb5LwWnyyg",
          "mode": "list",
          "cachedResultName": "$BTC OR $ETH Sentimen Media Sosial",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1Lma1X-KY3cEMbCLJEKKEChgYMPlppMGNTBb5LwWnyyg/edit?usp=drivesdk"
        },
        "sheetName": {
          "__rl": true,
          "value": "gid=0",
          "mode": "list",
          "cachedResultName": "Data Mentah",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1Lma1X-KY3cEMbCLJEKKEChgYMPlppMGNTBb5LwWnyyg/edit#gid=0"
        },
        "options": {}
      },
      "type": "n8n-nodes-base.googleSheets",
      "typeVersion": 4.7,
      "position": [
        208,
        384
      ],
      "id": "a46853d8-f229-4481-b999-f6950d211265",
      "name": "baca data",
      "credentials": {
        "googleSheetsOAuth2Api": {
          "id": "1i4CpejrRiWAa25G",
          "name": "Google Sheets account 3"
        }
      }
    },
    {
      "parameters": {
        "jsCode": "// Ambil semua baris dari node \"Google Sheets\"\n// **Pastikan nama node Anda adalah \"Google Sheets\"**\nconst items = $items(\"baca data\");\n\nlet positive = 0;\nlet negative = 0;\nlet neutral = 0;\nlet total = 0;\n\n// Loop melalui setiap baris\nfor (const item of items) {\n  // Ambil nilai dari kolom \"Sentiment\"\n  const sentiment = item.json.Sentiment;\n  \n  if (sentiment === 'Positive') {\n    positive++;\n  } else if (sentiment === 'Negative') {\n    negative++;\n  } else if (sentiment === 'Neutral') {\n    neutral++;\n  }\n}\n\ntotal = items.length;\n\n// Kembalikan hasil perhitungan\nreturn {\n  total_tweets: total,\n  sentimen_positif: positive,\n  sentimen_negatif: negative,\n  sentimen_netral: neutral\n};"
      },
      "type": "n8n-nodes-base.code",
      "typeVersion": 2,
      "position": [
        416,
        384
      ],
      "id": "d4823e0d-b370-467c-8029-a4a75e346693",
      "name": "analisis data"
    },
    {
      "parameters": {
        "model": "liquid/lfm-2.5-1.2b-instruct:free",
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.lmChatOpenRouter",
      "typeVersion": 1,
      "position": [
        544,
        592
      ],
      "id": "ced5ebac-6c2c-4cda-9a98-65670fccc1aa",
      "name": "OpenRouter Chat Model1",
      "credentials": {
        "openRouterApi": {
          "id": "690Ovy8cCHBHAqHt",
          "name": "awa"
        }
      }
    },
    {
      "parameters": {
        "promptType": "define",
        "text": "=Anda adalah seorang analis sentimen media sosial.\nTuliskan kesimpulan singkat (dalam bahasa Indonesia) untuk laporan Telegram, berdasarkan data berikut:\n\n- Total Tweet Dianalisis: {{ $json.total_tweets }}\n- Sentimen Positif: {{ $json.sentimen_positif }}\n- Sentimen Negatif: {{ $json.sentimen_negatif }}\n- Sentimen Netral: {{ $json.sentimen_netral }}\n\nBerikan ringkasan singkat tentang apa arti angka-angka ini (misalnya, \"Sentimen hari ini cenderung positif,\" \"Ada banyak keraguan di pasar,\" dll.).",
        "batching": {}
      },
      "type": "@n8n/n8n-nodes-langchain.chainLlm",
      "typeVersion": 1.9,
      "position": [
        608,
        384
      ],
      "id": "62ccbaad-51f7-4bbc-ab11-33e17a46b758",
      "name": "membuat kesimpulan"
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
        960,
        384
      ],
      "id": "82aacc6c-405a-4a20-80c7-3777dfa334be",
      "name": "kirim laporan",
      "webhookId": "29b1cd7f-225a-488e-ade2-63cb643b67b2",
      "credentials": {
        "telegramApi": {
          "id": "UeW4rIKFaGuH61DK",
          "name": "bot renjeun"
        }
      }
    },
    {
      "parameters": {
        "mode": "raw",
        "jsonOutput": "{\n  \"BTC\": {\n    \"total\": 90,\n    \"bullish\": 31,\n    \"bearish\": 33,\n    \"neutral\": 26,\n    \"avg_compound\": -0.0254,\n    \"signal\": \"NEUTRAL\",\n    \"scraped_at\": \"2026-04-22T03:09:25.128900\"\n  },\n  \"ETH\": {\n    \"total\": 75,\n    \"bullish\": 30,\n    \"bearish\": 32,\n    \"neutral\": 13,\n    \"avg_compound\": -0.0352,\n    \"signal\": \"NEUTRAL\",\n    \"scraped_at\": \"2026-04-22T03:09:25.129666\"\n  }\n}",
        "options": {}
      },
      "type": "n8n-nodes-base.set",
      "typeVersion": 3.4,
      "position": [
        208,
        0
      ],
      "id": "66e9acf8-2b45-4b20-a918-15dd71f4d73c",
      "name": "Edit Fields"
    }
  ],
  "connections": {
    "tiap 15 menit": {
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
    "analisis sentimen": {
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
    "OpenRouter Chat Model": {
      "ai_languageModel": [
        [
          {
            "node": "analisis sentimen",
            "type": "ai_languageModel",
            "index": 0
          }
        ]
      ]
    },
    "tiap jam 7 pagi": {
      "main": [
        [
          {
            "node": "baca data",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "baca data": {
      "main": [
        [
          {
            "node": "analisis data",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "analisis data": {
      "main": [
        [
          {
            "node": "membuat kesimpulan",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "OpenRouter Chat Model1": {
      "ai_languageModel": [
        [
          {
            "node": "membuat kesimpulan",
            "type": "ai_languageModel",
            "index": 0
          }
        ]
      ]
    },
    "membuat kesimpulan": {
      "main": [
        [
          {
            "node": "kirim laporan",
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
