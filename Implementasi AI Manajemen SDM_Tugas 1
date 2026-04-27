{
  "nodes": [
    {
      "parameters": {
        "listId": "69ee1cd051829678019c6d85",
        "name": "Checklist Onboarding",
        "additionalFields": {}
      },
      "type": "n8n-nodes-base.trello",
      "typeVersion": 1,
      "position": [
        368,
        0
      ],
      "id": "4d8b877a-9f98-434a-9253-da745aac52a8",
      "name": "Create a card",
      "credentials": {
        "trelloApi": {
          "id": "WLkIxpH6cyl7N0Ko",
          "name": "Trello account"
        }
      }
    },
    {
      "parameters": {
        "resource": "checklist",
        "operation": "create",
        "cardId": {
          "__rl": true,
          "value": "={{ $('Create a card').all()[0].json.id }}",
          "mode": "id"
        },
        "name": "=Daftar Tugas Onboarding",
        "additionalFields": {}
      },
      "type": "n8n-nodes-base.trello",
      "typeVersion": 1,
      "position": [
        736,
        0
      ],
      "id": "d9340c67-2f24-4c90-8d53-9a911ff738f9",
      "name": "Create a checklist",
      "credentials": {
        "trelloApi": {
          "id": "WLkIxpH6cyl7N0Ko",
          "name": "Trello account"
        }
      }
    },
    {
      "parameters": {
        "jsCode": "return [\n  {\n    json: {\n      checklist: $('Checklist').all().map(i => i.json['Checklist Onboarding Karyawan']),\n      sheet: $('Sheet Onboarding Karyawan').first().json\n    }\n  }\n];\n"
      },
      "type": "n8n-nodes-base.code",
      "typeVersion": 2,
      "position": [
        944,
        0
      ],
      "id": "9181359a-ce6b-44d0-8795-f2835e00e395",
      "name": "gabung jadi 1"
    },
    {
      "parameters": {
        "sendTo": "=salwabila12720@gmail.com",
        "subject": "=Selamat Datang di Perusahaan, {{ $json.sheet['First Name'] }} {{ $json.sheet['Last Name'] }}",
        "message": "=Hi {{ $json.sheet['First Name'] }}{{ $json.sheet['Last Name'] }}, \n\nSelamat datang di Perusahaan! Kami sangat senang Anda bergabung sebagai {{ $json.sheet.Position }} mulai {{ new Date(( $json.start_date - 25569) * 86400 * 1000).toLocaleDateString('id-ID') }}. \n\nBerikut daftar tugas onboarding Anda:\n<ul>\n  <li>{{ $json.checklist[0] }}</li>\n  <li>{{ $json.checklist[1] }}</li>\n  <li>{{ $json.checklist[2] }}</li>\n  <li>{{ $json.checklist[3] }}</li>\n  <li>{{ $json.checklist[4] }}</li>\n  <li>{{ $json.checklist[5] }}</li>\n</ul>\n\nJika ada pertanyaan, reply email ini. \n\nSalam, \nTim HR",
        "options": {}
      },
      "type": "n8n-nodes-base.gmail",
      "typeVersion": 2.2,
      "position": [
        1152,
        0
      ],
      "id": "7420c48c-3739-4b5d-8788-91b9d9c80f05",
      "name": "Send a message",
      "webhookId": "9cb5c130-1dfc-4f77-bc0c-f3be38552679",
      "credentials": {
        "gmailOAuth2": {
          "id": "hmMIdCyXQA9NBJ1J",
          "name": "akun nf"
        }
      }
    },
    {
      "parameters": {
        "pollTimes": {
          "item": [
            {
              "mode": "everyMinute"
            }
          ]
        },
        "documentId": {
          "__rl": true,
          "value": "1imZkJzQ7I5GhmipXX2waeLJvfLSzcht8TcFzrQ418uM",
          "mode": "list",
          "cachedResultName": "Copy of Onboarding Karyawan Baru (Jawaban)",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1imZkJzQ7I5GhmipXX2waeLJvfLSzcht8TcFzrQ418uM/edit?usp=drivesdk"
        },
        "sheetName": {
          "__rl": true,
          "value": 1373179962,
          "mode": "list",
          "cachedResultName": "Form Responses 1",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1imZkJzQ7I5GhmipXX2waeLJvfLSzcht8TcFzrQ418uM/edit#gid=1373179962"
        },
        "options": {}
      },
      "type": "n8n-nodes-base.googleSheetsTrigger",
      "typeVersion": 1,
      "position": [
        0,
        0
      ],
      "id": "c130c548-b21e-4079-8a87-1f5bc43986a9",
      "name": "Sheet Onboarding Karyawan",
      "credentials": {
        "googleSheetsTriggerOAuth2Api": {
          "id": "L9ck8gpiIc0Tljxo",
          "name": "Google Sheets Trigger account"
        }
      }
    },
    {
      "parameters": {
        "assignments": {
          "assignments": [
            {
              "id": "444a30e9-8492-4e2c-b368-02a365417034",
              "name": "first_name",
              "value": "={{ $('Sheet Onboarding Karyawan').item.json['First Name'] }}",
              "type": "string"
            },
            {
              "id": "30ebd616-6d65-426d-86ba-b0fe2883d802",
              "name": "last_name",
              "value": "={{ $json[\"Last Name\"] }}",
              "type": "string"
            },
            {
              "id": "ff349ddb-111c-4a79-a7dd-5f8f70083f0b",
              "name": "full_name",
              "value": "={{ $json[\"Full Name\"] }}",
              "type": "string"
            },
            {
              "id": "c65ffac4-8be5-4443-93e6-9fd87d11320d",
              "name": "email",
              "value": "={{ $json.Email }}",
              "type": "string"
            },
            {
              "id": "c4e60976-fa5c-4148-9e08-e981846ed2f4",
              "name": "start_date",
              "value": "={{ $json[\"Start Date\"] }}",
              "type": "number"
            },
            {
              "id": "82053950-5983-485f-8e40-25d45adf825e",
              "name": "position",
              "value": "={{ $json.Position }}",
              "type": "string"
            }
          ]
        },
        "options": {}
      },
      "type": "n8n-nodes-base.set",
      "typeVersion": 3.4,
      "position": [
        192,
        0
      ],
      "id": "4591fccd-7165-4faf-b9d6-184da91bed49",
      "name": "Data Normalization"
    },
    {
      "parameters": {
        "documentId": {
          "__rl": true,
          "value": "1imZkJzQ7I5GhmipXX2waeLJvfLSzcht8TcFzrQ418uM",
          "mode": "list",
          "cachedResultName": "Copy of Onboarding Karyawan Baru (Jawaban)",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1imZkJzQ7I5GhmipXX2waeLJvfLSzcht8TcFzrQ418uM/edit?usp=drivesdk"
        },
        "sheetName": {
          "__rl": true,
          "value": 138018800,
          "mode": "list",
          "cachedResultName": "Checklist",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1imZkJzQ7I5GhmipXX2waeLJvfLSzcht8TcFzrQ418uM/edit#gid=138018800"
        },
        "options": {}
      },
      "type": "n8n-nodes-base.googleSheets",
      "typeVersion": 4.7,
      "position": [
        528,
        0
      ],
      "id": "d3dbed19-f3cf-4a8b-b5f2-f918e021d105",
      "name": "Checklist",
      "credentials": {
        "googleSheetsOAuth2Api": {
          "id": "1i4CpejrRiWAa25G",
          "name": "Google Sheets account 3"
        }
      }
    }
  ],
  "connections": {
    "Create a card": {
      "main": [
        [
          {
            "node": "Checklist",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Create a checklist": {
      "main": [
        [
          {
            "node": "gabung jadi 1",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "gabung jadi 1": {
      "main": [
        [
          {
            "node": "Send a message",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Sheet Onboarding Karyawan": {
      "main": [
        [
          {
            "node": "Data Normalization",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Data Normalization": {
      "main": [
        [
          {
            "node": "Create a card",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Checklist": {
      "main": [
        [
          {
            "node": "Create a checklist",
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
