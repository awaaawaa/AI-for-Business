{
  "nodes": [
    {
      "parameters": {
        "formTitle": "Formulir Pengajuan Cuti",
        "formDescription": "Silahkan isi detail cuti anda. Patikan tanggal sesuai.",
        "formFields": {
          "values": [
            {
              "fieldLabel": "Email Karyawan",
              "requiredField": true
            },
            {
              "fieldLabel": "Jenis Cuti",
              "fieldType": "dropdown",
              "fieldOptions": {
                "values": [
                  {
                    "option": "Cuti Tahunan"
                  },
                  {
                    "option": "Cuti Sakit"
                  },
                  {
                    "option": "Cuti Tanpa Bayaran"
                  }
                ]
              }
            },
            {
              "fieldLabel": "Tanggal Mulai",
              "fieldType": "date",
              "requiredField": true
            },
            {
              "fieldLabel": "Tanggal Selesai",
              "fieldType": "date",
              "requiredField": true
            },
            {
              "fieldLabel": "Alasan/Keterangan",
              "fieldType": "textarea",
              "requiredField": true
            }
          ]
        },
        "options": {}
      },
      "type": "n8n-nodes-base.formTrigger",
      "typeVersion": 2.5,
      "position": [
        0,
        0
      ],
      "id": "9980c48d-f9bc-498a-9433-2c3e45746601",
      "name": "On form submission",
      "webhookId": "ac39cb4e-10d0-4043-9da7-af6deabc05da"
    },
    {
      "parameters": {
        "documentId": {
          "__rl": true,
          "value": "1tDsoQ9RZBavJZogYk9pw-DTw55Nr3icgPLrgjZOGm-k",
          "mode": "list",
          "cachedResultName": "Copy of Cuti Karyawan",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1tDsoQ9RZBavJZogYk9pw-DTw55Nr3icgPLrgjZOGm-k/edit?usp=drivesdk"
        },
        "sheetName": {
          "__rl": true,
          "value": "gid=0",
          "mode": "list",
          "cachedResultName": "DB_Karyawan",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1tDsoQ9RZBavJZogYk9pw-DTw55Nr3icgPLrgjZOGm-k/edit#gid=0"
        },
        "filtersUI": {
          "values": [
            {
              "lookupColumn": "Email",
              "lookupValue": "={{ $json['Email Karyawan'] }}"
            }
          ]
        },
        "options": {}
      },
      "type": "n8n-nodes-base.googleSheets",
      "typeVersion": 4.7,
      "position": [
        208,
        0
      ],
      "id": "055abd6e-e2ec-4ac6-bc87-525bcf67222c",
      "name": "Baca Sheet BD_Karyawan",
      "credentials": {
        "googleSheetsOAuth2Api": {
          "id": "1i4CpejrRiWAa25G",
          "name": "Google Sheets account 3"
        }
      }
    },
    {
      "parameters": {
        "jsCode": "// 1. Ambil Data dari Node Google Sheets (Input node ini)\n// Asumsi: Node Google Sheets mengembalikan 1 item (data karyawan ybs)\nconst employeeData = items[0].json;\n\n// 2. Ambil Data dari Node Form (Node sebelumnya)\n// Pastikan nama Node Form di dalam kurung $('...') SAMA PERSIS dengan nama node Anda\nconst formData = $('On form submission').first().json;\n\n// 3. Proses Tanggal menggunakan Luxon (LANGSUNG DIPAKAI)\n// Pastikan field di form Anda benar: \"Tanggal Mulai\" dan \"Tanggal Selesai\"\nconst start = DateTime.fromISO(formData[\"Tanggal Mulai\"]);\nconst end = DateTime.fromISO(formData[\"Tanggal Selesai\"]);\n\n// Hitung durasi (selisih hari + 1 agar inklusif)\nconst durationInDays = end.diff(start, 'days').days + 1;\n\n// 4. Logika Validasi Saldo\n// Pastikan kolom di Google Sheet bernama \"Saldo_Cuti\"\nconst currentBalance = parseInt(employeeData[\"Saldo_Cuti\"]); \nconst hasEnoughBalance = currentBalance >= durationInDays;\n\n// Generate ID Unik (Gabungan waktu + random biar tidak kembar)\nconst uniqueId = 'REQ-' + Date.now(); \n\nreturn [\n  {\n    json: {\n      ...employeeData,\n      ...formData,\n      durationRequested: durationInDays,\n      isApprovedSystem: hasEnoughBalance,\n      message: hasEnoughBalance ? \"Saldo Cukup\" : \"Saldo Tidak Cukup\",\n      requestId: uniqueId // <--- Field Baru\n    }\n  }\n];"
      },
      "type": "n8n-nodes-base.code",
      "typeVersion": 2,
      "position": [
        416,
        0
      ],
      "id": "96a77f58-ae5e-46b9-a2c5-5a75d5a12b4d",
      "name": "Validasi Cuti"
    },
    {
      "parameters": {
        "operation": "appendOrUpdate",
        "documentId": {
          "__rl": true,
          "value": "1tDsoQ9RZBavJZogYk9pw-DTw55Nr3icgPLrgjZOGm-k",
          "mode": "list",
          "cachedResultName": "Copy of Cuti Karyawan",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1tDsoQ9RZBavJZogYk9pw-DTw55Nr3icgPLrgjZOGm-k/edit?usp=drivesdk"
        },
        "sheetName": {
          "__rl": true,
          "value": 637903758,
          "mode": "list",
          "cachedResultName": "Log Pengajuan",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1tDsoQ9RZBavJZogYk9pw-DTw55Nr3icgPLrgjZOGm-k/edit#gid=637903758"
        },
        "columns": {
          "mappingMode": "defineBelow",
          "value": {
            "ID_Request": "={{ $json.requestId }}",
            "Timestamp": "={{ $json.submittedAt }}",
            "Email_Karyawan": "={{ $json['Email Karyawan'] }}",
            "Jenis_Cuti": "={{ $json['Jenis Cuti'] }}",
            "Tanggal_Mulai": "={{ $json['Tanggal Mulai'] }}",
            "Tanggal_Selesai": "={{ $json['Tanggal Selesai'] }}",
            "Durasi": "={{ $json.durationRequested }}",
            "Alasan": "={{ $json['Alasan/Keterangan'] }}",
            "Status": "Pending"
          },
          "matchingColumns": [
            "ID_Request"
          ],
          "schema": [
            {
              "id": "ID_Request",
              "displayName": "ID_Request",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": false
            },
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
              "id": "Email_Karyawan",
              "displayName": "Email_Karyawan",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "Jenis_Cuti",
              "displayName": "Jenis_Cuti",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "Tanggal_Mulai",
              "displayName": "Tanggal_Mulai",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "Tanggal_Selesai",
              "displayName": "Tanggal_Selesai",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "Durasi",
              "displayName": "Durasi",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "Alasan",
              "displayName": "Alasan",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "Status",
              "displayName": "Status",
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
        624,
        0
      ],
      "id": "4f483512-5e6f-44ab-b9f1-b625926e0ad3",
      "name": "Update Sheet Log",
      "credentials": {
        "googleSheetsOAuth2Api": {
          "id": "1i4CpejrRiWAa25G",
          "name": "Google Sheets account 3"
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
              "id": "a9a2bc40-6fc9-4ddc-8e44-b0acebd31cb7",
              "leftValue": "={{ $('Validasi Cuti').item.json.isApprovedSystem.toString() }}",
              "rightValue": "=true",
              "operator": {
                "type": "string",
                "operation": "contains"
              }
            },
            {
              "id": "d4ec1be1-7448-4516-ba14-9c79ae4d7521",
              "leftValue": "={{ $('Validasi Cuti').item.json.isApprovedSystem }}",
              "rightValue": "=false",
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
        832,
        0
      ],
      "id": "d2b7d4b5-9de0-4a2c-bc59-1f38e3b055e2",
      "name": "If"
    },
    {
      "parameters": {
        "sendTo": "={{ $('Validasi Cuti').item.json.Manager_Email }}",
        "subject": "Permohonan Cuti",
        "message": "=<p>Halo Manager,</p>\n<p>Ada pengajuan cuti baru yang membutuhkan persetujuan Anda:</p>\n<ul>\n  <li><strong>Nama:</strong> {{ $('Validasi Cuti').item.json.Nama_Lengkap }}</li>\n  <li><strong>Email:</strong> {{ $('Validasi Cuti').item.json['Email Karyawan'] }}</li>\n  <li><strong>Tanggal:</strong> {{ $('Validasi Cuti').item.json['Tanggal Mulai'] }} s.d {{ $('Validasi Cuti').item.json['Tanggal Selesai'] }}</li>\n  <li><strong>Total Durasi:</strong> {{ $('Validasi Cuti').item.json.durationRequested }} Hari</li>\n  <li><strong>Alasan:</strong> {{ $('Validasi Cuti').item.json['Alasan/Keterangan'] }}</li>\n</ul>\n<p>Silakan klik keputusan Anda:</p>\n<p>\n  <a href=\"https://n8n-o1nh8ige3xml.jkt3.sumopod.my.id/webhook-test/approval-handler?status=approved&email={{ $('Validasi Cuti').item.json['Email Karyawan'] }}&days={{ $('Validasi Cuti').item.json.durationRequested }}&id={{ $('Validasi Cuti').item.json.requestId }}\" \n     style=\"background-color: #4CAF50; color: white; padding: 10px 20px; text-decoration: none; border-radius: 5px; font-weight: bold; margin-right: 15px; display: inline-block;\">\n     ✅ SETUJUI\n  </a>\n  <a href=\"https://n8n-o1nh8ige3xml.jkt3.sumopod.my.id/webhook-test/approval-handler?status=rejected&email={{ $('Validasi Cuti').item.json['Email Karyawan'] }}&days={{ $('Validasi Cuti').item.json.durationRequested }}&id={{ $('Validasi Cuti').item.json.requestId }}\" \n     style=\"background-color: #f44336; color: white; padding: 10px 20px; text-decoration: none; border-radius: 5px; font-weight: bold; display: inline-block;\">\n     ✖️ TOLAK\n  </a>\n</p>\n<p><small>Link ini menggunakan environment TEST. Pastikan n8n workflow 'Approval Handler' sedang aktif (Listen for test event) saat diklik.</small></p>",
        "options": {}
      },
      "type": "n8n-nodes-base.gmail",
      "typeVersion": 2.2,
      "position": [
        1040,
        -96
      ],
      "id": "8a3e4bf7-58c8-4190-abc7-6e2e24fec405",
      "name": "Email Diterima",
      "webhookId": "8bc5a2b3-e153-4594-9019-21a9cc0ae9a7",
      "credentials": {
        "gmailOAuth2": {
          "id": "hmMIdCyXQA9NBJ1J",
          "name": "akun nf"
        }
      }
    },
    {
      "parameters": {
        "sendTo": "={{ $('On form submission').item.json['Email Karyawan'] }}",
        "subject": "Pengajuan Cuti Ditolak - Saldo Tidak Cukup",
        "message": "=Halo ,{{ $('Validasi Cuti').item.json.Nama_Lengkap }}  Pengajuan cuti Anda untuk tanggal {{ $('Validasi Cuti').item.json['Tanggal Mulai'] }} s/d {{ $('Validasi Cuti').item.json['Tanggal Selesai'] }} DITOLAK secara otomatis oleh sistem.  Alasan: Sisa saldo cuti Anda ({{ $json.Saldo_Cuti }} hari) tidak mencukupi untuk pengajuan {{ $('Validasi Cuti').item.json.durationRequested }} hari.  Salam, HR Bot",
        "options": {}
      },
      "type": "n8n-nodes-base.gmail",
      "typeVersion": 2.2,
      "position": [
        1040,
        96
      ],
      "id": "8091fdb5-8645-44f1-80d0-01f705fa973f",
      "name": "Email Cuti Tidak Cukup",
      "webhookId": "b49f01eb-f1a7-4f02-a23c-02e4edeaab15",
      "credentials": {
        "gmailOAuth2": {
          "id": "hmMIdCyXQA9NBJ1J",
          "name": "akun nf"
        }
      }
    },
    {
      "parameters": {
        "path": "approval-handler",
        "responseMode": "responseNode",
        "options": {}
      },
      "type": "n8n-nodes-base.webhook",
      "typeVersion": 2.1,
      "position": [
        0,
        448
      ],
      "id": "2351d7ae-b826-4c98-a0b6-1223f5beee63",
      "name": "Webhook",
      "webhookId": "405c4245-bf81-4323-a624-4396f1dd883d"
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
              "id": "099281a4-db20-4676-bf8b-76794b44c276",
              "leftValue": "={{ $json.query.status }}",
              "rightValue": "approved",
              "operator": {
                "type": "string",
                "operation": "equals",
                "name": "filter.operator.equals"
              }
            }
          ],
          "combinator": "and"
        },
        "options": {}
      },
      "type": "n8n-nodes-base.if",
      "typeVersion": 2.3,
      "position": [
        208,
        448
      ],
      "id": "d0dfaebb-f435-4d8f-bc17-c1a87efff2f1",
      "name": "If1"
    },
    {
      "parameters": {
        "documentId": {
          "__rl": true,
          "value": "1tDsoQ9RZBavJZogYk9pw-DTw55Nr3icgPLrgjZOGm-k",
          "mode": "list",
          "cachedResultName": "Copy of Cuti Karyawan",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1tDsoQ9RZBavJZogYk9pw-DTw55Nr3icgPLrgjZOGm-k/edit?usp=drivesdk"
        },
        "sheetName": {
          "__rl": true,
          "value": "gid=0",
          "mode": "list",
          "cachedResultName": "DB_Karyawan",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1tDsoQ9RZBavJZogYk9pw-DTw55Nr3icgPLrgjZOGm-k/edit#gid=0"
        },
        "filtersUI": {
          "values": [
            {
              "lookupColumn": "Email",
              "lookupValue": "={{ $json.query.email }}"
            }
          ]
        },
        "options": {}
      },
      "type": "n8n-nodes-base.googleSheets",
      "typeVersion": 4.7,
      "position": [
        416,
        352
      ],
      "id": "6ac19cc9-ed20-418d-bae6-957f213f9667",
      "name": "Cari Data Karyawan",
      "credentials": {
        "googleSheetsOAuth2Api": {
          "id": "1i4CpejrRiWAa25G",
          "name": "Google Sheets account 3"
        }
      }
    },
    {
      "parameters": {
        "jsCode": "// 1. Ambil data dari Webhook (Node paling awal)\n// Kita butuh 'days' (jumlah hari cuti) yang dikirim lewat URL\nconst webhookData = $('Webhook').first().json.query;\nconst daysRequested = parseInt(webhookData.days);\n\n// 2. Ambil data dari Google Sheets (Node sebelumnya)\n// Kita butuh 'Saldo_Cuti' saat ini\nconst currentData = items[0].json;\nconst currentBalance = parseInt(currentData.Saldo_Cuti);\n\n// 3. Hitung Saldo Baru\nconst newBalance = currentBalance - daysRequested;\n\n// 4. Return data untuk update\nreturn [{\n  json: {\n    ...currentData, // Bawa semua data lama (termasuk row_number)\n    newBalance: newBalance\n  }\n}];"
      },
      "type": "n8n-nodes-base.code",
      "typeVersion": 2,
      "position": [
        624,
        352
      ],
      "id": "136c5406-dff4-4ef7-a121-c1c3880c0748",
      "name": "Hitung Saldo Baru"
    },
    {
      "parameters": {
        "operation": "update",
        "documentId": {
          "__rl": true,
          "value": "1tDsoQ9RZBavJZogYk9pw-DTw55Nr3icgPLrgjZOGm-k",
          "mode": "list",
          "cachedResultName": "Copy of Cuti Karyawan",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1tDsoQ9RZBavJZogYk9pw-DTw55Nr3icgPLrgjZOGm-k/edit?usp=drivesdk"
        },
        "sheetName": {
          "__rl": true,
          "value": "gid=0",
          "mode": "list",
          "cachedResultName": "DB_Karyawan",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1tDsoQ9RZBavJZogYk9pw-DTw55Nr3icgPLrgjZOGm-k/edit#gid=0"
        },
        "columns": {
          "mappingMode": "defineBelow",
          "value": {
            "Email": "={{ $json.Email }}",
            "Saldo_Cuti": "={{ $json.newBalance }}",
            "row_number": 0
          },
          "matchingColumns": [
            "Email"
          ],
          "schema": [
            {
              "id": "Email",
              "displayName": "Email",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": false
            },
            {
              "id": "Nama_Lengkap",
              "displayName": "Nama_Lengkap",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "Saldo_Cuti",
              "displayName": "Saldo_Cuti",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "Manager_Email",
              "displayName": "Manager_Email",
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
        832,
        352
      ],
      "id": "0e571e01-19a7-4060-854e-19b51e3a98d0",
      "name": "Update Saldo Cuti",
      "credentials": {
        "googleSheetsOAuth2Api": {
          "id": "1i4CpejrRiWAa25G",
          "name": "Google Sheets account 3"
        }
      }
    },
    {
      "parameters": {
        "operation": "appendOrUpdate",
        "documentId": {
          "__rl": true,
          "value": "1tDsoQ9RZBavJZogYk9pw-DTw55Nr3icgPLrgjZOGm-k",
          "mode": "list",
          "cachedResultName": "Copy of Cuti Karyawan",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1tDsoQ9RZBavJZogYk9pw-DTw55Nr3icgPLrgjZOGm-k/edit?usp=drivesdk"
        },
        "sheetName": {
          "__rl": true,
          "value": 637903758,
          "mode": "list",
          "cachedResultName": "Log Pengajuan",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1tDsoQ9RZBavJZogYk9pw-DTw55Nr3icgPLrgjZOGm-k/edit#gid=637903758"
        },
        "columns": {
          "mappingMode": "defineBelow",
          "value": {
            "ID_Request": "={{ $('Webhook').item.json.query.id }}",
            "Status": "Approved"
          },
          "matchingColumns": [
            "ID_Request"
          ],
          "schema": [
            {
              "id": "ID_Request",
              "displayName": "ID_Request",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": false
            },
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
              "id": "Email_Karyawan",
              "displayName": "Email_Karyawan",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "Jenis_Cuti",
              "displayName": "Jenis_Cuti",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "Tanggal_Mulai",
              "displayName": "Tanggal_Mulai",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "Tanggal_Selesai",
              "displayName": "Tanggal_Selesai",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "Durasi",
              "displayName": "Durasi",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "Alasan",
              "displayName": "Alasan",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "Status",
              "displayName": "Status",
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
        1040,
        352
      ],
      "id": "66837dd0-ef5e-4133-a3cc-4ea0463c7906",
      "name": "Update Logs",
      "credentials": {
        "googleSheetsOAuth2Api": {
          "id": "1i4CpejrRiWAa25G",
          "name": "Google Sheets account 3"
        }
      }
    },
    {
      "parameters": {
        "respondWith": "text",
        "responseBody": "Berhasil!! Pengajuan cuti telah disetujui. Saldo karyawan sudah dipotong otomatis",
        "options": {}
      },
      "type": "n8n-nodes-base.respondToWebhook",
      "typeVersion": 1.5,
      "position": [
        1216,
        352
      ],
      "id": "f95d7548-a6e1-4567-9ce7-24444e3da576",
      "name": "Respond to Webhook"
    },
    {
      "parameters": {
        "sendTo": "={{ $('Update Saldo Cuti').item.json.Email}}",
        "subject": "✅Pengajuan Cuti DISETUJUI",
        "message": "=Halo,  Kabar baik! Pengajuan cuti Anda telah DISETUJUI oleh Manager.  Detail: - Durasi: {{ $('Webhook').item.json.query.days }} Hari - Status: APPROVED - Saldo Cuti: Telah dipotong otomatis.  Terima kasih, HR System",
        "options": {}
      },
      "type": "n8n-nodes-base.gmail",
      "typeVersion": 2.2,
      "position": [
        1424,
        352
      ],
      "id": "aaa3ce2b-f689-4329-b24e-f103c29c52eb",
      "name": "Cuti Diterima",
      "webhookId": "7e66ad65-21e5-418f-8bb1-e63f0988ed00",
      "credentials": {
        "gmailOAuth2": {
          "id": "hmMIdCyXQA9NBJ1J",
          "name": "akun nf"
        }
      }
    },
    {
      "parameters": {
        "sendTo": "={{ $('Webhook').item.json.query.email }}",
        "subject": "Status Pengajuan Cuti: DITOLAK",
        "message": "=Halo,  Mohon maaf, pengajuan cuti Anda untuk durasi {{ $('Webhook').item.json.query.days }} hari telah DITOLAK oleh Manager.  Silakan hubungi atasan Anda untuk diskusi lebih lanjut.  Salam, HR System",
        "options": {}
      },
      "type": "n8n-nodes-base.gmail",
      "typeVersion": 2.2,
      "position": [
        416,
        512
      ],
      "id": "3d1ee1dc-c1b4-4743-a78d-33ebf17d7613",
      "name": "Cuti Ditolak",
      "webhookId": "d3b80360-583a-41ff-b9d1-4443610bc21c",
      "credentials": {
        "gmailOAuth2": {
          "id": "hmMIdCyXQA9NBJ1J",
          "name": "akun nf"
        }
      }
    },
    {
      "parameters": {
        "respondWith": "text",
        "responseBody": "Konfirmasi: Pengajuan cuti telah berhasil DITOLAK. Tidak ada saldo yang dipotong.",
        "options": {}
      },
      "type": "n8n-nodes-base.respondToWebhook",
      "typeVersion": 1.5,
      "position": [
        624,
        512
      ],
      "id": "c873b59f-dd9c-40bd-9a56-6ab008a195c4",
      "name": "Respond to Webhook1"
    },
    {
      "parameters": {
        "operation": "appendOrUpdate",
        "documentId": {
          "__rl": true,
          "value": "1tDsoQ9RZBavJZogYk9pw-DTw55Nr3icgPLrgjZOGm-k",
          "mode": "list",
          "cachedResultName": "Copy of Cuti Karyawan",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1tDsoQ9RZBavJZogYk9pw-DTw55Nr3icgPLrgjZOGm-k/edit?usp=drivesdk"
        },
        "sheetName": {
          "__rl": true,
          "value": 637903758,
          "mode": "list",
          "cachedResultName": "Log Pengajuan",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1tDsoQ9RZBavJZogYk9pw-DTw55Nr3icgPLrgjZOGm-k/edit#gid=637903758"
        },
        "columns": {
          "mappingMode": "defineBelow",
          "value": {
            "ID_Request": "={{ $('Webhook').item.json.query.id }}",
            "Status": "Rejected"
          },
          "matchingColumns": [
            "ID_Request"
          ],
          "schema": [
            {
              "id": "ID_Request",
              "displayName": "ID_Request",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": false
            },
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
              "id": "Email_Karyawan",
              "displayName": "Email_Karyawan",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "Jenis_Cuti",
              "displayName": "Jenis_Cuti",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "Tanggal_Mulai",
              "displayName": "Tanggal_Mulai",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "Tanggal_Selesai",
              "displayName": "Tanggal_Selesai",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "Durasi",
              "displayName": "Durasi",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "Alasan",
              "displayName": "Alasan",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "Status",
              "displayName": "Status",
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
        832,
        512
      ],
      "id": "2bb1553f-5b84-446b-9853-82c970daacd5",
      "name": "Append or update row in sheet",
      "credentials": {
        "googleSheetsOAuth2Api": {
          "id": "1i4CpejrRiWAa25G",
          "name": "Google Sheets account 3"
        }
      }
    }
  ],
  "connections": {
    "On form submission": {
      "main": [
        [
          {
            "node": "Baca Sheet BD_Karyawan",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Baca Sheet BD_Karyawan": {
      "main": [
        [
          {
            "node": "Validasi Cuti",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Validasi Cuti": {
      "main": [
        [
          {
            "node": "Update Sheet Log",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Update Sheet Log": {
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
            "node": "Email Diterima",
            "type": "main",
            "index": 0
          }
        ],
        [
          {
            "node": "Email Cuti Tidak Cukup",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Webhook": {
      "main": [
        [
          {
            "node": "If1",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "If1": {
      "main": [
        [
          {
            "node": "Cari Data Karyawan",
            "type": "main",
            "index": 0
          }
        ],
        [
          {
            "node": "Cuti Ditolak",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Cari Data Karyawan": {
      "main": [
        [
          {
            "node": "Hitung Saldo Baru",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Hitung Saldo Baru": {
      "main": [
        [
          {
            "node": "Update Saldo Cuti",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Update Saldo Cuti": {
      "main": [
        [
          {
            "node": "Update Logs",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Update Logs": {
      "main": [
        [
          {
            "node": "Respond to Webhook",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Respond to Webhook": {
      "main": [
        [
          {
            "node": "Cuti Diterima",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Cuti Ditolak": {
      "main": [
        [
          {
            "node": "Respond to Webhook1",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Respond to Webhook1": {
      "main": [
        [
          {
            "node": "Append or update row in sheet",
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
