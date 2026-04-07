{
  "nodes": [
    {
      "parameters": {
        "amount": 10
      },
      "type": "n8n-nodes-base.wait",
      "typeVersion": 1.1,
      "position": [
        592,
        0
      ],
      "id": "fe2593ba-75d7-4c7b-92a5-3977b5b6e292",
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
        784,
        0
      ],
      "id": "8587c787-19d4-4d1f-aafb-b407341baa7f",
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
        944,
        0
      ],
      "id": "f61b68f2-4997-412c-af2a-2a138745cece",
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
        240,
        0
      ],
      "id": "41b8c9bd-4b39-42c8-aad5-ffa59e016cde",
      "name": "On form submission",
      "webhookId": "d1944bcd-f65b-4698-bdfd-10cb752ce73c"
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
        "jsonBody": "{\n  \"model\": \"grok-imagine/text-to-image\",\n  \"input\": {\n    \"prompt\": \"{{ $json.prompt.replace(/\\\"/g, '\\\\\\\"') }}\",\n    \"aspect_ratio\": \"3:2\"\n  }\n}",
        "options": {}
      },
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 4.4,
      "position": [
        416,
        0
      ],
      "id": "cab378da-7b5b-43dc-a54d-53d96839e4e6",
      "name": "Mengirim Image Generation ke KIE.AI.API"
    },
    {
      "parameters": {
        "jsCode": "const result = JSON.parse($json.data.resultJson);\n\nreturn [{\n  img1: result.resultUrls[0] || null,\n  img2: result.resultUrls[1] || null,\n  img3: result.resultUrls[2] || null,\n  img4: result.resultUrls[3] || null\n}];\n"
      },
      "type": "n8n-nodes-base.code",
      "typeVersion": 2,
      "position": [
        1184,
        -16
      ],
      "id": "79c66c38-613b-4747-aaf4-0ded8641f2a6",
      "name": "Format Result"
    },
    {
      "parameters": {
        "jsCode": "const urls = [\n  $json.img1,\n  $json.img2,\n  $json.img3,\n  $json.img4\n].filter(Boolean);\n\n// jadikan 1 URL = 1 item\nreturn urls.map((url, index) => ({\n  json: {\n    url,\n    index: index + 1\n  }\n}));\n\n"
      },
      "type": "n8n-nodes-base.code",
      "typeVersion": 2,
      "position": [
        1360,
        -16
      ],
      "id": "0174dcc8-0929-43d8-8cab-798d97a01098",
      "name": "loop image"
    },
    {
      "parameters": {
        "url": "={{ $json.url }}",
        "options": {}
      },
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 4.4,
      "position": [
        1568,
        -16
      ],
      "id": "90049099-523e-4bce-b9ec-0117c1166046",
      "name": "HTTP Request"
    },
    {
      "parameters": {
        "operation": "sendPhoto",
        "chatId": "8740336461",
        "binaryData": true,
        "additionalFields": {}
      },
      "type": "n8n-nodes-base.telegram",
      "typeVersion": 1.2,
      "position": [
        1776,
        -16
      ],
      "id": "c7d4f5b1-c7c9-4023-ae9f-763aa5ecbb2b",
      "name": "Send a photo message",
      "webhookId": "b5b49478-9474-4a3b-bc5c-689c746fce6e",
      "credentials": {
        "telegramApi": {
          "id": "UtqIjuBUVwAiDzWL",
          "name": "bot jaemin"
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
            "node": "Format Result",
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
    "Format Result": {
      "main": [
        [
          {
            "node": "loop image",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "loop image": {
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
            "node": "Send a photo message",
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
