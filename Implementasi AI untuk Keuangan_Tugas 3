{
  "nodes": [
    {
      "parameters": {
        "rule": {
          "interval": [
            {
              "triggerAtHour": 8
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
      "id": "f2428b33-d0c4-4d23-8702-a9cfdff60aa3",
      "name": "Schedule Trigger"
    },
    {
      "parameters": {
        "documentId": {
          "__rl": true,
          "value": "1tNbd2cQ-cCQ9QYcBT5XyXwJkGGlUVrZoPYoJuXqYITI",
          "mode": "list",
          "cachedResultName": "Copy of Dummy Keuangan 1",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1tNbd2cQ-cCQ9QYcBT5XyXwJkGGlUVrZoPYoJuXqYITI/edit?usp=drivesdk"
        },
        "sheetName": {
          "__rl": true,
          "value": "gid=0",
          "mode": "list",
          "cachedResultName": "Sheet1",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1tNbd2cQ-cCQ9QYcBT5XyXwJkGGlUVrZoPYoJuXqYITI/edit#gid=0"
        },
        "options": {}
      },
      "type": "n8n-nodes-base.googleSheets",
      "typeVersion": 4.7,
      "position": [
        224,
        -144
      ],
      "id": "5644ab9d-2944-4939-8185-cddc34f21cb4",
      "name": "data 1",
      "credentials": {
        "googleSheetsOAuth2Api": {
          "id": "1i4CpejrRiWAa25G",
          "name": "Google Sheets account 3"
        }
      }
    },
    {
      "parameters": {
        "documentId": {
          "__rl": true,
          "value": "1JgWrl6gqShhND2HLMMCgk3VeNprt02CF4Mgib2G4epw",
          "mode": "list",
          "cachedResultName": "Copy of Dummy Keuangan 2",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1JgWrl6gqShhND2HLMMCgk3VeNprt02CF4Mgib2G4epw/edit?usp=drivesdk"
        },
        "sheetName": {
          "__rl": true,
          "value": 1840720130,
          "mode": "list",
          "cachedResultName": "Sheet2",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1JgWrl6gqShhND2HLMMCgk3VeNprt02CF4Mgib2G4epw/edit#gid=1840720130"
        },
        "options": {}
      },
      "type": "n8n-nodes-base.googleSheets",
      "typeVersion": 4.7,
      "position": [
        224,
        0
      ],
      "id": "5857356f-5c40-4255-b7ef-1cde389dfe4d",
      "name": "data 2",
      "credentials": {
        "googleSheetsOAuth2Api": {
          "id": "1i4CpejrRiWAa25G",
          "name": "Google Sheets account 3"
        }
      }
    },
    {
      "parameters": {
        "documentId": {
          "__rl": true,
          "value": "1YifZJCCsPf50Y58cTPH_u0BTIRGjuO16rL7COycq-Ic",
          "mode": "list",
          "cachedResultName": "Copy of Dummy Keuangan 3",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1YifZJCCsPf50Y58cTPH_u0BTIRGjuO16rL7COycq-Ic/edit?usp=drivesdk"
        },
        "sheetName": {
          "__rl": true,
          "value": 257652098,
          "mode": "list",
          "cachedResultName": "Sheet3",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1YifZJCCsPf50Y58cTPH_u0BTIRGjuO16rL7COycq-Ic/edit#gid=257652098"
        },
        "options": {}
      },
      "type": "n8n-nodes-base.googleSheets",
      "typeVersion": 4.7,
      "position": [
        224,
        160
      ],
      "id": "cb49680e-8058-48d4-a952-e0a264039b17",
      "name": "data 3",
      "credentials": {
        "googleSheetsOAuth2Api": {
          "id": "1i4CpejrRiWAa25G",
          "name": "Google Sheets account 3"
        }
      }
    },
    {
      "parameters": {},
      "type": "n8n-nodes-base.merge",
      "typeVersion": 3.2,
      "position": [
        432,
        -144
      ],
      "id": "833734c2-85e2-47d0-91ca-36f6b86597ff",
      "name": "Merge"
    },
    {
      "parameters": {
        "jsCode": "const items = $input.all();\n\nitems.forEach(item => {\n  if (item.json && item.json['ID Laporan']) {\n    // Tambahkan kolom \"Sumber\" berdasarkan ID awal\n    if (item.json['ID Laporan'].startsWith('REP')) {\n      item.json.Sumber = 'Sheet1';\n    } else if (item.json['ID Laporan'].startsWith('LAP')) {\n      item.json.Sumber = 'Sheet2';\n    } else {\n      item.json.Sumber = 'Unknown';\n    }\n  }\n});\n\nreturn items;\n"
      },
      "type": "n8n-nodes-base.code",
      "typeVersion": 2,
      "position": [
        624,
        -144
      ],
      "id": "18a2245a-3032-4ab7-ae78-8d309f8180aa",
      "name": "menambahkan kolom sumber"
    },
    {
      "parameters": {
        "compare": "selectedFields",
        "fieldsToCompare": "ID Laporan",
        "options": {}
      },
      "type": "n8n-nodes-base.removeDuplicates",
      "typeVersion": 2,
      "position": [
        832,
        -144
      ],
      "id": "9f21f91c-e9bb-4398-b1fb-ee0c3e7c20a2",
      "name": "menghapus duplikat"
    },
    {
      "parameters": {
        "jsCode": "// Ambil semua item dari input (aman untuk semua mode)\nconst inputData = $input.all();\n\n// Ekstrak semua baris dari semua item\nconst allRows = inputData.flatMap(item =>\n  Array.isArray(item.json) ? item.json : [item.json]\n);\n\n// Proses tiap baris\nallRows.forEach(row => {\n  if (typeof row === 'object' && row !== null) {\n    if (row['ID Laporan']) row['ID Laporan'] = String(row['ID Laporan']).trim();\n    if (row.Bulan) row.Bulan = String(row.Bulan).trim();\n    if (row['Kategori Produk']) row['Kategori Produk'] = String(row['Kategori Produk']).trim();\n    if (row['Nama Produk']) row['Nama Produk'] = String(row['Nama Produk']).trim();\n\n    row['Jumlah Stok'] = parseFloat(row['Jumlah Stok']) || 0;\n    row['Penjualan Harian'] = parseFloat(row['Penjualan Harian']) || 0;\n    row['Harga Satuan (IDR)'] = parseFloat(row['Harga Satuan (IDR)']) || 0;\n    row['Total Penjualan (IDR)'] = parseFloat(row['Total Penjualan (IDR)']) || 0;\n  }\n});\n\n// Kembalikan sebagai daftar item terpisah\nreturn allRows.map(row => ({ json: row }));\n"
      },
      "type": "n8n-nodes-base.code",
      "typeVersion": 2,
      "position": [
        432,
        160
      ],
      "id": "c21d9c12-9154-4b35-a482-93f7dc1cde33",
      "name": "Code in JavaScript"
    },
    {
      "parameters": {
        "compare": "selectedFields",
        "fieldsToCompare": "ID Laporan",
        "options": {}
      },
      "type": "n8n-nodes-base.removeDuplicates",
      "typeVersion": 2,
      "position": [
        640,
        160
      ],
      "id": "983e20fa-f9a7-4fa6-9003-a1e353364ff4",
      "name": "Remove Duplicates"
    },
    {
      "parameters": {
        "jsCode": "// Ambil semua input (untuk aman di semua mode)\nconst inputData = $input.all();\n\n// Ekstrak semua baris\nconst allRows = inputData.flatMap(item =>\n  Array.isArray(item.json) ? item.json : [item.json]\n);\n\n// Transformasi setiap baris\nconst transformedRows = allRows.map(row => {\n  // Gabung Kategori + Nama Produk untuk kolom \"Produk\"\n  const produk = `${row['Kategori Produk'] || ''} ${row['Nama Produk'] || ''}`.trim();\n\n  // Buat objek baru dengan format Sheet 1 & 2\n  return {\n    'ID Laporan': row['ID Laporan'] ? String(row['ID Laporan']).trim() : '',\n    'Bulan': row.Bulan ? String(row.Bulan).trim() : '',\n    'Produk': produk,\n    'Wilayah': '-', // default, bisa diisi jika ada info wilayah\n    'Penjualan (Unit)': parseFloat(row['Penjualan Harian']) || 0,\n    'Target (Unit)': 0, // default, bisa diisi jika ada target\n    'Pendapatan (IDR)': parseFloat(row['Total Penjualan (IDR)']) || 0,\n    'Status': row['Karyawan Penanggung Jawab'] ? String(row['Karyawan Penanggung Jawab']).trim() : 'Tidak Diketahui',\n    'Keterangan': row['Catatan Status'] ? String(row['Catatan Status']).trim() : '',\n    'Tanggal Laporan': row.Bulan ? `${row.Bulan} 01, ${new Date().getFullYear()}` : ''\n  };\n});\n\n// Kembalikan sebagai array item terpisah\nreturn transformedRows.map(row => ({ json: row }));\n"
      },
      "type": "n8n-nodes-base.code",
      "typeVersion": 2,
      "position": [
        848,
        160
      ],
      "id": "548e7d42-1a4b-447f-8a1e-7a32bc46b0ac",
      "name": "menyesuaikan header"
    },
    {
      "parameters": {
        "jsCode": "const items = $input.all();\n\nitems.forEach(item => {\n  if (item.json && item.json['ID Laporan']) {\n    // Tambahkan kolom \"Sumber\" berdasarkan ID awal\n    if (item.json['ID Laporan'].startsWith('REP')) {\n      item.json.Sumber = 'Sheet1';\n    } else if (item.json['ID Laporan'].startsWith('LAP')) {\n      item.json.Sumber = 'Sheet2';\n    } else {\n      item.json.Sumber = 'Unknown';\n    }\n  }\n});\n\nreturn items;"
      },
      "type": "n8n-nodes-base.code",
      "typeVersion": 2,
      "position": [
        1056,
        160
      ],
      "id": "646eab07-f525-4268-ba35-0495229063ef",
      "name": "menambahkan kolom"
    },
    {
      "parameters": {
        "mode": "combine",
        "combineBy": "combineByPosition",
        "options": {}
      },
      "type": "n8n-nodes-base.merge",
      "typeVersion": 3.2,
      "position": [
        1536,
        144
      ],
      "id": "ccba627a-0d3f-4a93-bb70-ebf1afdd649b",
      "name": "gabung jadi 1"
    },
    {
      "parameters": {
        "jsCode": "// Ambil SEMUA input dari semua jalur\nconst allInputs = $input.all();\n\n// Gabungkan semua baris dari semua input\nconst allRows = allInputs.flatMap(item =>\n  Array.isArray(item.json) ? item.json : [item.json]\n);\n\n// Filter hanya bulan ini\nconst now = new Date();\nconst currentMonthName = now.toLocaleString('id-ID', { month: 'long' });\nconst currentYear = now.getFullYear();\n\nconst monthlyData = allRows.filter(row => \n  String(row.Bulan || '').toLowerCase() === currentMonthName.toLowerCase()\n);\n\n// Hitung metrik\nconst totalPenjualanUnit = monthlyData.reduce((sum, r) => sum + (r['Penjualan (Unit)'] || 0), 0);\nconst totalPendapatan = monthlyData.reduce((sum, r) => sum + (r['Pendapatan (IDR)'] || 0), 0);\nconst totalLaporan = monthlyData.length;\n\n// Buat ringkasan\nconst laporan = {\n  'Bulan': currentMonthName,\n  'Tahun': currentYear,\n  'Jumlah_Laporan': totalLaporan,\n  'Total_Penjualan_Unit': totalPenjualanUnit,\n  'Total_Pendapatan_IDR': totalPendapatan,\n  'Rata_Rata_Penjualan_Per_Laporan': totalLaporan ? (totalPenjualanUnit / totalLaporan).toFixed(2) : 0,\n  'Rata_Rata_Pendapatan_Per_Laporan': totalLaporan ? (totalPendapatan / totalLaporan).toFixed(2) : 0,\n  'Sumber_Data': 'Sheet 1, Sheet 2, Sheet 3',\n  'Terakhir_Diperbarui': new Date().toISOString()\n};\n\n// Kembalikan HANYA 1 item\nreturn [{ json: laporan }];\n"
      },
      "type": "n8n-nodes-base.code",
      "typeVersion": 2,
      "position": [
        1744,
        144
      ],
      "id": "d34b80e2-1dc9-465d-ac51-a2470b6b4a2d",
      "name": "generate laporan"
    },
    {
      "parameters": {
        "operation": "appendOrUpdate",
        "documentId": {
          "__rl": true,
          "value": "1mly6YDiNwxF05mGRrblha611mlARXIRg60KnopFIsZc",
          "mode": "list",
          "cachedResultName": "Dummy master sheets",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1mly6YDiNwxF05mGRrblha611mlARXIRg60KnopFIsZc/edit?usp=drivesdk"
        },
        "sheetName": {
          "__rl": true,
          "value": 1513503370,
          "mode": "list",
          "cachedResultName": "Sheet2",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1mly6YDiNwxF05mGRrblha611mlARXIRg60KnopFIsZc/edit#gid=1513503370"
        },
        "columns": {
          "mappingMode": "autoMapInputData",
          "value": {},
          "matchingColumns": [],
          "schema": [
            {
              "id": "Bulan",
              "displayName": "Bulan",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "Total Pemasukan",
              "displayName": "Total Pemasukan",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "Total pengeluaran",
              "displayName": "Total pengeluaran",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "Saldo Akhir",
              "displayName": "Saldo Akhir",
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
        1936,
        -16
      ],
      "id": "e80441b4-68aa-436b-85ca-d9089a167a78",
      "name": "Append or update row in sheet1",
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
        "text": "=📊 *Laporan Bulanan — {{$json.Bulan}} {{$json.Tahun}}*  ✅ *Jumlah Laporan*: {{$json.Jumlah_Laporan}} 📦 *Penjualan Total*: {{$json.Total_Penjualan_Unit}} unit 💰 *Pendapatan*: Rp{{ $json.Total_Pendapatan_IDR }}  📈 *Rata-rata Penjualan*: {{$json.Rata_Rata_Penjualan_Per_Laporan}} unit/laporan   📎 [Laporan Detail](https://docs.google.com/spreadsheets/d/1XgSB7caGKoqvUDOu00fJljwLOxscyEmvxuzQWkVJiFU/edit?usp=sharing)",
        "additionalFields": {}
      },
      "type": "n8n-nodes-base.telegram",
      "typeVersion": 1.2,
      "position": [
        1936,
        144
      ],
      "id": "cb376bb5-b5b0-44aa-b88f-309da27612aa",
      "name": "Send a text message",
      "webhookId": "cce05103-9d8e-4e3d-84bf-18386ff45fca",
      "credentials": {
        "telegramApi": {
          "id": "UeW4rIKFaGuH61DK",
          "name": "bot renjeun"
        }
      }
    },
    {
      "parameters": {
        "sendTo": "salwabila12720@gmail.com",
        "subject": "Laporan Keuangan Bulanan",
        "message": "=<!DOCTYPE html> <html> <head>   <style>     body { font-family: Arial, sans-serif; line-height: 1.6; }     .header { background: #0d47a1; color: white; padding: 15px; text-align: center; }     .content { padding: 20px; }     .metric { margin: 8px 0; font-weight: bold; }     .highlight { color: #1976d2; }   </style> </head> <body>   <div class=\"header\">     <h2>📊 Laporan Bulanan</h2>     <p>{{ $json.Bulan }} {{ $json.Tahun }}</p>   </div>   <div class=\"content\">     <p>Halo Tim,</p>     <p>Berikut ringkasan laporan bulanan dari data gabungan (Sheet 1, 2, dan 3):</p>          <div class=\"metric\">✅ Jumlah Laporan: <span class=\"highlight\">{{ $json.Jumlah_Laporan }}</span></div>     <div class=\"metric\">📦 Total Penjualan: <span class=\"highlight\">{{ $json.Total_Penjualan_Unit }} unit</span></div>     <div class=\"metric\">💰 Total Pendapatan: <span class=\"highlight\">Rp{{ $json.Total_Pendapatan_IDR }}</span></div>     <div class=\"metric\">📈 Rata-rata Penjualan/Laporan: <span class=\"highlight\">{{ $json.Rata_Rata_Penjualan_Per_Laporan }} unit</span></div>          <p>🔗 <a href=\"https://docs.google.com/spreadsheets/d/1XgSB7caGKoqvUDOu00fJljwLOxscyEmvxuzQWkVJiFU/edit?usp=sharing/d/...\">Lihat Master Sheet</a> \n <a href=\"https://docs.google.com/spreadsheets/d/1XgSB7caGKoqvUDOu00fJljwLOxscyEmvxuzQWkVJiFU/edit?usp=sharing/...\">Lihat Laporan Bulanan</a></p>            </div> </body> </html>",
        "options": {}
      },
      "type": "n8n-nodes-base.gmail",
      "typeVersion": 2.2,
      "position": [
        1936,
        288
      ],
      "id": "2baaf70d-c3ab-4c5d-b4a3-6ea3a5e99561",
      "name": "Send a message",
      "webhookId": "2d1c6a37-48b1-473b-94c0-e6ed01c834ff",
      "credentials": {
        "gmailOAuth2": {
          "id": "hmMIdCyXQA9NBJ1J",
          "name": "Gmail account"
        }
      }
    },
    {
      "parameters": {
        "operation": "appendOrUpdate",
        "documentId": {
          "__rl": true,
          "value": "1mly6YDiNwxF05mGRrblha611mlARXIRg60KnopFIsZc",
          "mode": "list",
          "cachedResultName": "Dummy master sheets",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1mly6YDiNwxF05mGRrblha611mlARXIRg60KnopFIsZc/edit?usp=drivesdk"
        },
        "sheetName": {
          "__rl": true,
          "value": "gid=0",
          "mode": "list",
          "cachedResultName": "Sheet1",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1mly6YDiNwxF05mGRrblha611mlARXIRg60KnopFIsZc/edit#gid=0"
        },
        "columns": {
          "mappingMode": "autoMapInputData",
          "value": {},
          "matchingColumns": [
            "ID Laporan"
          ],
          "schema": [
            {
              "id": "ID Laporan",
              "displayName": "ID Laporan",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": false
            },
            {
              "id": "Bulan",
              "displayName": "Bulan",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
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
            },
            {
              "id": "Wilayah",
              "displayName": "Wilayah",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": false
            },
            {
              "id": "Penjualan (Unit)",
              "displayName": "Penjualan (Unit)",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": false
            },
            {
              "id": "Target (Unit)",
              "displayName": "Target (Unit)",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": false
            },
            {
              "id": "Pendapatan (IDR)",
              "displayName": "Pendapatan (IDR)",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": false
            },
            {
              "id": "Status",
              "displayName": "Status",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": false
            },
            {
              "id": "Keterangan",
              "displayName": "Keterangan",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": false
            },
            {
              "id": "Tanggal Laporan",
              "displayName": "Tanggal Laporan",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": false
            },
            {
              "id": "Sumber",
              "displayName": "Sumber",
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
        1312,
        -144
      ],
      "id": "b9c370cc-6f9b-4ecf-bdfc-47d9875169e5",
      "name": "tulis ke sheet master",
      "credentials": {
        "googleSheetsOAuth2Api": {
          "id": "1i4CpejrRiWAa25G",
          "name": "Google Sheets account 3"
        }
      }
    }
  ],
  "connections": {
    "Schedule Trigger": {
      "main": [
        [
          {
            "node": "data 1",
            "type": "main",
            "index": 0
          },
          {
            "node": "data 2",
            "type": "main",
            "index": 0
          },
          {
            "node": "data 3",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "data 1": {
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
    "data 2": {
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
    "data 3": {
      "main": [
        [
          {
            "node": "Code in JavaScript",
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
            "node": "menambahkan kolom sumber",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "menambahkan kolom sumber": {
      "main": [
        [
          {
            "node": "menghapus duplikat",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "menghapus duplikat": {
      "main": [
        [
          {
            "node": "tulis ke sheet master",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Code in JavaScript": {
      "main": [
        [
          {
            "node": "Remove Duplicates",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Remove Duplicates": {
      "main": [
        [
          {
            "node": "menyesuaikan header",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "menyesuaikan header": {
      "main": [
        [
          {
            "node": "menambahkan kolom",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "menambahkan kolom": {
      "main": [
        [
          {
            "node": "tulis ke sheet master",
            "type": "main",
            "index": 0
          },
          {
            "node": "gabung jadi 1",
            "type": "main",
            "index": 1
          }
        ]
      ]
    },
    "gabung jadi 1": {
      "main": [
        [
          {
            "node": "generate laporan",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "generate laporan": {
      "main": [
        [
          {
            "node": "Append or update row in sheet1",
            "type": "main",
            "index": 0
          },
          {
            "node": "Send a text message",
            "type": "main",
            "index": 0
          },
          {
            "node": "Send a message",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "tulis ke sheet master": {
      "main": [
        [
          {
            "node": "gabung jadi 1",
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
