{
  "nodes": [
    {
      "parameters": {
        "options": {}
      },
      "type": "n8n-nodes-base.emailReadImap",
      "typeVersion": 2.1,
      "position": [
        0,
        16
      ],
      "id": "5e0ad2ba-b18e-4979-af20-481378edf877",
      "name": "Email Trigger (IMAP)",
      "credentials": {
        "imap": {
          "id": "qertrziT53oIpEZ9",
          "name": "akun google salwabila12720"
        }
      }
    },
    {
      "parameters": {
        "rules": {
          "values": [
            {
              "conditions": {
                "options": {
                  "caseSensitive": false,
                  "leftValue": "",
                  "typeValidation": "strict",
                  "version": 3
                },
                "conditions": [
                  {
                    "leftValue": "={{ $json.from }}",
                    "rightValue": "siti23083si",
                    "operator": {
                      "type": "string",
                      "operation": "contains"
                    },
                    "id": "a5db0c32-f8d8-4eb0-8ef2-02b7d9b56538"
                  }
                ],
                "combinator": "and"
              },
              "renameOutput": true,
              "outputKey": "IDCloudHost"
            },
            {
              "conditions": {
                "options": {
                  "caseSensitive": false,
                  "leftValue": "",
                  "typeValidation": "strict",
                  "version": 3
                },
                "conditions": [
                  {
                    "id": "bbfa66f9-c286-404e-9180-f539f76ce263",
                    "leftValue": "={{ $json.from }}",
                    "rightValue": "asyawa728",
                    "operator": {
                      "type": "string",
                      "operation": "contains"
                    }
                  }
                ],
                "combinator": "and"
              },
              "renameOutput": true,
              "outputKey": "Grab"
            },
            {
              "conditions": {
                "options": {
                  "caseSensitive": false,
                  "leftValue": "",
                  "typeValidation": "strict",
                  "version": 3
                },
                "conditions": [
                  {
                    "id": "165cf0f2-89d2-40d8-bf36-f045310ec69d",
                    "leftValue": "={{ $json.from }}",
                    "rightValue": "choipangsitchoi",
                    "operator": {
                      "type": "string",
                      "operation": "contains"
                    }
                  }
                ],
                "combinator": "and"
              },
              "renameOutput": true,
              "outputKey": "Tokopedia"
            }
          ]
        },
        "options": {
          "ignoreCase": true
        }
      },
      "type": "n8n-nodes-base.switch",
      "typeVersion": 3.4,
      "position": [
        208,
        0
      ],
      "id": "30133b9d-c039-49c4-9065-a25053419912",
      "name": "Switch"
    },
    {
      "parameters": {
        "numberInputs": 3
      },
      "type": "n8n-nodes-base.merge",
      "typeVersion": 3.2,
      "position": [
        656,
        0
      ],
      "id": "9da899e8-3fb1-4a76-b126-a0b51515d2bb",
      "name": "Merge"
    },
    {
      "parameters": {
        "operation": "append",
        "documentId": {
          "__rl": true,
          "value": "1sKAz6JyUUy_cNTkHCRKYIFx2AowCwitRPh6ox4ovoNI",
          "mode": "list",
          "cachedResultName": "Pencatat Keuangan dari Email",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1sKAz6JyUUy_cNTkHCRKYIFx2AowCwitRPh6ox4ovoNI/edit?usp=drivesdk"
        },
        "sheetName": {
          "__rl": true,
          "value": "gid=0",
          "mode": "list",
          "cachedResultName": "Sheet1",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1sKAz6JyUUy_cNTkHCRKYIFx2AowCwitRPh6ox4ovoNI/edit#gid=0"
        },
        "columns": {
          "mappingMode": "defineBelow",
          "value": {
            "Tanggal": "={{ $json.Tanggal }}",
            "Jumlah ": "={{ $json.Jumlah }}",
            "Produk": "={{ $json.Nominal }}"
          },
          "matchingColumns": [],
          "schema": [
            {
              "id": "Tanggal",
              "displayName": "Tanggal",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": false
            },
            {
              "id": "Jumlah ",
              "displayName": "Jumlah ",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": false
            },
            {
              "id": "Produk",
              "displayName": "Produk",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
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
        864,
        16
      ],
      "id": "211d0cd5-0f67-4c76-b84e-effae259928d",
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
        "assignments": {
          "assignments": [
            {
              "id": "2d40aaf4-1ba6-4e7b-8292-6eee3cbbdf00",
              "name": "Tanggal",
              "value": "{{ $('Menunggu dan mengambil email baru').item.json.date }}",
              "type": "string"
            },
            {
              "id": "b0d21d1d-c55a-4a5c-a949-3aad61af83c3",
              "name": "Jumlah",
              "value": "{{ $json.textPlain.match(/Total.*?Rp\\s*([ \\d\\.]+)/s)?.[1].replace(/\\./g, '') }}",
              "type": "string"
            },
            {
              "id": "323452a7-e855-4080-8ab2-941b4601a4e9",
              "name": "Nominal",
              "value": "cloud",
              "type": "string"
            }
          ]
        },
        "options": {}
      },
      "type": "n8n-nodes-base.set",
      "typeVersion": 3.4,
      "position": [
        432,
        -144
      ],
      "id": "e9b0e6c7-9770-475b-ae32-271f87590a66",
      "name": "IDCloudHost"
    },
    {
      "parameters": {
        "assignments": {
          "assignments": [
            {
              "id": "f24e9f3e-2b7a-4af8-b2de-59cf292fe9e3",
              "name": "Tanggal",
              "value": "={{ $json.date }}",
              "type": "string"
            },
            {
              "id": "5ece3ec4-8d67-4204-8830-34606f0212a2",
              "name": "Jumlah",
              "value": "{{ $json.textPlain.match(/Total Tarif.*?([\\d\\.]+)/s)?.[1].replace(/\\./g, '') }}",
              "type": "string"
            },
            {
              "id": "3da47685-0673-47a3-80c9-a58c68ab46f4",
              "name": "Nominal",
              "value": "Grab",
              "type": "string"
            }
          ]
        },
        "options": {}
      },
      "type": "n8n-nodes-base.set",
      "typeVersion": 3.4,
      "position": [
        432,
        16
      ],
      "id": "76132146-578e-4902-80d4-35e8b96cb026",
      "name": "Grab"
    },
    {
      "parameters": {
        "assignments": {
          "assignments": [
            {
              "id": "96dfeecf-fbcc-4568-a60f-f216c29d47d2",
              "name": "Tanggal",
              "value": "={{ $json.date }}",
              "type": "string"
            },
            {
              "id": "9a3b81a5-52dc-4214-9765-8335e78efff3",
              "name": "Jumlah",
              "value": "{{ $json.textPlain.match(/Harga\\s*Rp([\\d\\.]+)/)?.[1].replace(/\\./g, '') }}",
              "type": "string"
            },
            {
              "id": "448990dc-92dd-4cf5-9e94-39c4a0b757dc",
              "name": "Nominal",
              "value": "{{ $json.textPlain.match(/Nominal\\s*(.*?)\\s*Waktu/s)?.[1].trim() }}",
              "type": "string"
            }
          ]
        },
        "options": {}
      },
      "type": "n8n-nodes-base.set",
      "typeVersion": 3.4,
      "position": [
        432,
        144
      ],
      "id": "c7012fbc-f78b-422d-8959-70b2a749fcdb",
      "name": "Tokopedia"
    }
  ],
  "connections": {
    "Email Trigger (IMAP)": {
      "main": [
        [
          {
            "node": "Switch",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Switch": {
      "main": [
        [
          {
            "node": "IDCloudHost",
            "type": "main",
            "index": 0
          }
        ],
        [
          {
            "node": "Grab",
            "type": "main",
            "index": 0
          }
        ],
        [
          {
            "node": "Tokopedia",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Merge": {
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
    "IDCloudHost": {
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
    "Grab": {
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
    "Tokopedia": {
      "main": [
        [
          {
            "node": "Merge",
            "type": "main",
            "index": 2
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
