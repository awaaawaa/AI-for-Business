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
      "id": "76556dbd-5fe6-4245-943f-61335a941924",
      "name": "Schedule Trigger"
    },
    {
      "parameters": {
        "documentId": {
          "__rl": true,
          "value": "10q3-FxDMZOxepA9tGTpstSdJK1BrMkujH6yZlKZh2lE",
          "mode": "list",
          "cachedResultName": "Copy of Auto Posting Scheduler",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/10q3-FxDMZOxepA9tGTpstSdJK1BrMkujH6yZlKZh2lE/edit?usp=drivesdk"
        },
        "sheetName": {
          "__rl": true,
          "value": "gid=0",
          "mode": "list",
          "cachedResultName": "Sheet1",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/10q3-FxDMZOxepA9tGTpstSdJK1BrMkujH6yZlKZh2lE/edit#gid=0"
        },
        "options": {}
      },
      "type": "n8n-nodes-base.googleSheets",
      "typeVersion": 4.7,
      "position": [
        208,
        0
      ],
      "id": "0b9635cf-f91b-4df6-a265-72571c31c7b3",
      "name": "Get row(s) in sheet",
      "credentials": {
        "googleSheetsOAuth2Api": {
          "id": "1i4CpejrRiWAa25G",
          "name": "Google Sheets account 3"
        }
      }
    },
    {
      "parameters": {
        "chatId": "8740336461",
        "text": "{{ $json.Content }}",
        "additionalFields": {}
      },
      "type": "n8n-nodes-base.telegram",
      "typeVersion": 1.2,
      "position": [
        592,
        0
      ],
      "id": "3508ad32-b054-4a83-9e5a-8bdc81736522",
      "name": "Send a text message",
      "webhookId": "282e5fca-4f57-4546-9a78-13cf25f4fb39",
      "credentials": {
        "telegramApi": {
          "id": "UtqIjuBUVwAiDzWL",
          "name": "bot jaemin"
        }
      }
    },
    {
      "parameters": {
        "assignments": {
          "assignments": [
            {
              "id": "58c01fbc-f279-428b-8fc3-c6b720d9dee7",
              "name": "row_number",
              "value": "={{ $node[\"filter ready post\"].json.row_number }}",
              "type": "string"
            }
          ]
        },
        "options": {}
      },
      "type": "n8n-nodes-base.set",
      "typeVersion": 3.4,
      "position": [
        800,
        0
      ],
      "id": "26483f88-ee30-471f-8ce4-dd8f43526446",
      "name": "Edit Fields"
    },
    {
      "parameters": {
        "operation": "update",
        "documentId": {
          "__rl": true,
          "value": "10q3-FxDMZOxepA9tGTpstSdJK1BrMkujH6yZlKZh2lE",
          "mode": "list",
          "cachedResultName": "Copy of Auto Posting Scheduler",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/10q3-FxDMZOxepA9tGTpstSdJK1BrMkujH6yZlKZh2lE/edit?usp=drivesdk"
        },
        "sheetName": {
          "__rl": true,
          "value": "gid=0",
          "mode": "list",
          "cachedResultName": "Sheet1",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/10q3-FxDMZOxepA9tGTpstSdJK1BrMkujH6yZlKZh2lE/edit#gid=0"
        },
        "columns": {
          "mappingMode": "defineBelow",
          "value": {
            "ID": "={{ $json.row_number }}",
            "Status": "Published",
            "row_number": "={{ $json.row_number }}"
          },
          "matchingColumns": [
            "row_number"
          ],
          "schema": [
            {
              "id": "ID",
              "displayName": "ID",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "Content",
              "displayName": "Content",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": true
            },
            {
              "id": "Scheduled Date",
              "displayName": "Scheduled Date",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": true
            },
            {
              "id": "Scheduled Time",
              "displayName": "Scheduled Time",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": true
            },
            {
              "id": "Status",
              "displayName": "Status",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "row_number",
              "displayName": "row_number",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "number",
              "canBeUsedToMatch": true,
              "readOnly": true,
              "removed": false
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
        1008,
        0
      ],
      "id": "7f81be65-3576-410e-ae63-8fc4beaa3356",
      "name": "Update row in sheet",
      "credentials": {
        "googleSheetsOAuth2Api": {
          "id": "1i4CpejrRiWAa25G",
          "name": "Google Sheets account 3"
        }
      }
    },
    {
      "parameters": {
        "jsCode": "const now = DateTime.now().setZone('Asia/Jakarta');\nconst postsToSend = [];\n\nfor (const item of items) {\n  const row = item.json;\n  const dateStr = row['Scheduled Date']; \n  const timeStr = row['Scheduled Time']; \n\n  if (true) { // Paksa semua data lewat untuk tes\n    // Memvalidasi format dd/MM/yyyy H:mm:ss\n    const scheduledTime = DateTime.fromFormat(`${dateStr} ${timeStr}`, \"dd/MM/yyyy H:mm:ss\", { zone: 'Asia/Jakarta' });\n\n    // Jika waktu valid dan sudah lewat dari waktu sekarang\n    if (scheduledTime.isValid && scheduledTime <= now) {\n      postsToSend.push(item);\n    }\n  }\n}\nreturn postsToSend;"
      },
      "type": "n8n-nodes-base.code",
      "typeVersion": 2,
      "position": [
        384,
        0
      ],
      "id": "4a06c0ab-9836-4b5c-92c5-5e73adcf0431",
      "name": "filter ready post"
    }
  ],
  "connections": {
    "Schedule Trigger": {
      "main": [
        [
          {
            "node": "Get row(s) in sheet",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Get row(s) in sheet": {
      "main": [
        [
          {
            "node": "filter ready post",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Send a text message": {
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
    "Edit Fields": {
      "main": [
        [
          {
            "node": "Update row in sheet",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "filter ready post": {
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
