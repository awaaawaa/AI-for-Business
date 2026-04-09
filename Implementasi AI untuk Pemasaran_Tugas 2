{
  "nodes": [
    {
      "parameters": {
        "amount": 20
      },
      "type": "n8n-nodes-base.wait",
      "typeVersion": 1.1,
      "position": [
        -944,
        224
      ],
      "id": "f5493e79-b5ea-4491-aaf0-5eeff4d75ee3",
      "name": "Wait",
      "webhookId": "984aad59-54fc-46ee-8579-6c108156372d"
    },
    {
      "parameters": {
        "url": "https://api.kie.ai/api/v1/jobs/recordInfo",
        "sendQuery": true,
        "queryParameters": {
          "parameters": [
            {
              "name": "taskId",
              "value": "={{ $json.data.taskId }}"
            }
          ]
        },
        "sendHeaders": true,
        "headerParameters": {
          "parameters": [
            {
              "name": "Content-Type",
              "value": "application/json"
            },
            {
              "name": "Authorization",
              "value": "=Bearer {{ $('On form submission').item.json.api_key }}"
            }
          ]
        },
        "options": {}
      },
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 4.4,
      "position": [
        -752,
        224
      ],
      "id": "cd2ea5cd-40b0-4fa1-87ab-7dbae050c9a4",
      "name": "HTTP Request1"
    },
    {
      "parameters": {
        "conditions": {
          "options": {
            "caseSensitive": true,
            "leftValue": "",
            "typeValidation": "loose",
            "version": 3
          },
          "conditions": [
            {
              "id": "e7571566-c46b-4db0-b5c1-aba751a5e81a",
              "leftValue": "success",
              "rightValue": "={{ $json.data.state }}",
              "operator": {
                "type": "string",
                "operation": "contains"
              }
            }
          ],
          "combinator": "and"
        },
        "looseTypeValidation": true,
        "options": {}
      },
      "type": "n8n-nodes-base.if",
      "typeVersion": 2.3,
      "position": [
        -592,
        224
      ],
      "id": "46c9d40d-b637-43df-88dc-db421c0ba513",
      "name": "If"
    },
    {
      "parameters": {
        "formTitle": "Generate Gambar Konten Otomatis",
        "formFields": {
          "values": [
            {
              "fieldLabel": "prompt",
              "fieldName": "prompt"
            },
            {
              "fieldLabel": "task_type",
              "fieldName": "task_type",
              "placeholder": "mj_txt2img"
            },
            {
              "fieldLabel": "api_key",
              "fieldName": "api_key"
            }
          ]
        },
        "options": {}
      },
      "type": "n8n-nodes-base.formTrigger",
      "typeVersion": 2.5,
      "position": [
        -1296,
        224
      ],
      "id": "91fe26e6-b821-4755-8d60-ab2408c459a5",
      "name": "On form submission",
      "webhookId": "25960db0-1d1b-44a7-8555-60d8cdbe6ad3"
    },
    {
      "parameters": {
        "method": "POST",
        "url": "https://api.kie.ai/api/v1/jobs/createTask",
        "sendHeaders": true,
        "headerParameters": {
          "parameters": [
            {
              "name": "Content-Type",
              "value": "application/json"
            },
            {
              "name": "Authorization",
              "value": "=Bearer {{$json.api_key}}"
            }
          ]
        },
        "sendBody": true,
        "specifyBody": "json",
        "jsonBody": "={\n  \"model\": \"grok-imagine/image-to-video\",\n  \"input\": {\n    \"prompt\": \"{{ $json.prompt }}\",\n    \"mode\": \"normal\",\n    \"duration\": 6,\n    \"resolution\": \"480p\",\n    \"aspect_ratio\": \"2:3\",\n    \"nsfw_checker\": true\n  }\n}",
        "options": {}
      },
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 4.4,
      "position": [
        -1120,
        224
      ],
      "id": "43f2f63c-e6ca-44bf-b703-4a6ccaa43598",
      "name": "Mengirim Image Generation ke KIE.AI.API"
    },
    {
      "parameters": {
        "jsCode": "const input = $input.item.json;\nconst data = input.data || {};\nlet result = {};\n\ntry {\n    // Cek apakah resultJson itu string atau sudah jadi objek\n    result = typeof data.resultJson === 'string' ? JSON.parse(data.resultJson) : (data.resultJson || {});\n} catch (e) {\n    result = {};\n}\n\n// Mencoba berbagai kemungkinan nama field URL dari API\nconst videoUrl = result.resultUrls?.[0] || result.url || result.video_url || null;\n\nif (videoUrl) {\n    return [{ videoUrl: videoUrl }];\n}\n\n// JANGAN kirim null, kirim array kosong agar Download Video tidak jalan kalau URL belum ada\nreturn [];"
      },
      "type": "n8n-nodes-base.code",
      "typeVersion": 2,
      "position": [
        -384,
        208
      ],
      "id": "fe1fc834-d050-43c8-912f-46968f7375e5",
      "name": "Parse Video URL"
    },
    {
      "parameters": {
        "url": "={{ $json.videoUrl }}",
        "options": {
          "response": {
            "response": {}
          }
        }
      },
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 4.3,
      "position": [
        -176,
        208
      ],
      "id": "c0fe0c0c-31c6-4530-95fd-f4b3e34cb219",
      "name": "Download Video"
    },
    {
      "parameters": {
        "name": "Video Topik 3",
        "driveId": {
          "__rl": true,
          "value": "My Drive",
          "mode": "list",
          "cachedResultName": "My Drive",
          "cachedResultUrl": "https://drive.google.com/drive/my-drive"
        },
        "folderId": {
          "__rl": true,
          "value": "15l29ys4ZqmyqGb1z63g7jojZCfyItLmb",
          "mode": "list",
          "cachedResultName": "matkul awa",
          "cachedResultUrl": "https://drive.google.com/drive/folders/15l29ys4ZqmyqGb1z63g7jojZCfyItLmb"
        },
        "options": {}
      },
      "type": "n8n-nodes-base.googleDrive",
      "typeVersion": 3,
      "position": [
        32,
        208
      ],
      "id": "242d3cb4-409f-48a3-8996-4460c888cb46",
      "name": "Upload file",
      "credentials": {
        "googleDriveOAuth2Api": {
          "id": "7GFy8HsXrOHshTxF",
          "name": "akun nf"
        }
      }
    }
  ],
  "connections": {
    "Wait": {
      "main": [
        [
          {
            "node": "HTTP Request1",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "HTTP Request1": {
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
            "node": "Parse Video URL",
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
    "On form submission": {
      "main": [
        [
          {
            "node": "Mengirim Image Generation ke KIE.AI.API",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Mengirim Image Generation ke KIE.AI.API": {
      "main": [
        [
          {
            "node": "Wait",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Parse Video URL": {
      "main": [
        [
          {
            "node": "Download Video",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Download Video": {
      "main": [
        [
          {
            "node": "Upload file",
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
