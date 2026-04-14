{
  "nodes": [
    {
      "parameters": {},
      "type": "n8n-nodes-base.manualTrigger",
      "typeVersion": 1,
      "position": [
        0,
        0
      ],
      "id": "0adea496-ee25-46f6-9f89-8301ad870780",
      "name": "When clicking ‘Execute workflow’"
    },
    {
      "parameters": {
        "chatId": "1535237765",
        "text": "={{ $json.message }}",
        "additionalFields": {
          "parse_mode": "HTML"
        }
      },
      "type": "n8n-nodes-base.telegram",
      "typeVersion": 1.2,
      "position": [
        1248,
        0
      ],
      "id": "5fcd250b-6d36-4c80-bf8c-30203dd29d07",
      "name": "Send a text message",
      "webhookId": "a39a7cbb-6226-4a71-beae-75aa9f76c8d9",
      "credentials": {
        "telegramApi": {
          "id": "UeW4rIKFaGuH61DK",
          "name": "bot renjeun"
        }
      }
    },
    {
      "parameters": {
        "documentId": {
          "__rl": true,
          "value": "1xeeRzunECQL_5tJvwgpWcpQ0Zcq0Wjkj4j9x0taU2Lo",
          "mode": "list",
          "cachedResultName": "Copy of Best Time to Post Data",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1xeeRzunECQL_5tJvwgpWcpQ0Zcq0Wjkj4j9x0taU2Lo/edit?usp=drivesdk"
        },
        "sheetName": {
          "__rl": true,
          "value": "gid=0",
          "mode": "list",
          "cachedResultName": "Data Posting",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1xeeRzunECQL_5tJvwgpWcpQ0Zcq0Wjkj4j9x0taU2Lo/edit#gid=0"
        },
        "options": {}
      },
      "type": "n8n-nodes-base.googleSheets",
      "typeVersion": 4.7,
      "position": [
        208,
        0
      ],
      "id": "b8429eee-1afb-4b7b-8c3c-16e01b6d77cb",
      "name": "baca data posting",
      "credentials": {
        "googleSheetsOAuth2Api": {
          "id": "1i4CpejrRiWAa25G",
          "name": "Google Sheets account 3"
        }
      }
    },
    {
      "parameters": {
        "jsCode": "// Ambil semua data dari Google Sheets\nconst items = $input.all();\n\nconsole.log('Total items:', items.length);\n\n// Validasi data\nif (!items || items.length === 0) {\n  throw new Error('Tidak ada data yang dibaca dari Google Sheets!');\n}\n\n// Log sample data untuk debugging\nconsole.log('Sample first item:', JSON.stringify(items[0].json));\n\n// Object untuk menyimpan data per jam\nconst hourlyData = {};\n\n// Counter untuk tracking\nlet processedCount = 0;\nlet skippedCount = 0;\n\n// Proses setiap row data\nitems.forEach((item, index) => {\n  try {\n    // Get data dengan berbagai kemungkinan nama kolom\n    const rawData = item.json;\n    \n    // Coba berbagai nama kolom yang mungkin\n    const hour = rawData['Jam Posting'] || rawData['jam posting'] || rawData['Jam'] || rawData['jam'];\n    const likes = parseInt(rawData['Likes'] || rawData['likes'] || 0);\n    const comments = parseInt(rawData['Comments'] || rawData['comments'] || 0);\n    const shares = parseInt(rawData['Shares'] || rawData['shares'] || 0);\n    const platform = rawData['Platform'] || rawData['platform'] || 'Unknown';\n    \n    // Skip jika jam tidak valid atau undefined\n    if (hour === undefined || hour === null || hour === '') {\n      console.log(`Skipping row ${index + 1}: hour is undefined`);\n      skippedCount++;\n      return;\n    }\n    \n    // Convert hour ke number jika string\n    const hourNum = typeof hour === 'number' ? hour : parseInt(hour);\n    \n    // Validasi hour range (0-23)\n    if (isNaN(hourNum) || hourNum < 0 || hourNum > 23) {\n      console.log(`Skipping row ${index + 1}: invalid hour ${hour}`);\n      skippedCount++;\n      return;\n    }\n    \n    // Hitung total engagement (bobot: likes x1, comments x2, shares x3)\n    const engagement = likes + (comments * 2) + (shares * 3);\n    \n    // Initialize data untuk jam ini jika belum ada\n    if (!hourlyData[hourNum]) {\n      hourlyData[hourNum] = {\n        hour: hourNum,\n        totalEngagement: 0,\n        count: 0,\n        totalLikes: 0,\n        totalComments: 0,\n        totalShares: 0,\n        platforms: {}\n      };\n    }\n    \n    // Akumulasi data\n    hourlyData[hourNum].totalEngagement += engagement;\n    hourlyData[hourNum].count += 1;\n    hourlyData[hourNum].totalLikes += likes;\n    hourlyData[hourNum].totalComments += comments;\n    hourlyData[hourNum].totalShares += shares;\n    \n    // Track platform distribution\n    if (!hourlyData[hourNum].platforms[platform]) {\n      hourlyData[hourNum].platforms[platform] = 0;\n    }\n    hourlyData[hourNum].platforms[platform] += 1;\n    \n    processedCount++;\n    \n  } catch (error) {\n    console.error(`Error processing row ${index + 1}:`, error.message);\n    skippedCount++;\n  }\n});\n\nconsole.log(`Processed: ${processedCount}, Skipped: ${skippedCount}`);\n\n// Validasi hasil\nif (Object.keys(hourlyData).length === 0) {\n  throw new Error(`Tidak ada data valid yang bisa diproses! Processed: ${processedCount}, Skipped: ${skippedCount}`);\n}\n\n// Hitung rata-rata dan buat array\nconst results = Object.values(hourlyData).map(data => {\n  const mostUsedPlatform = Object.keys(data.platforms).reduce((a, b) => \n    data.platforms[a] > data.platforms[b] ? a : b\n  );\n  \n  return {\n    jam: `${String(data.hour).padStart(2, '0')}:00`,\n    avgEngagement: Math.round(data.totalEngagement / data.count),\n    jumlahPost: data.count,\n    avgLikes: Math.round(data.totalLikes / data.count),\n    avgComments: Math.round(data.totalComments / data.count),\n    avgShares: Math.round(data.totalShares / data.count),\n    platformTerbanyak: mostUsedPlatform,\n    engagementScore: Math.round((data.totalEngagement / data.count) * 100) / 100\n  };\n});\n\n// Sort berdasarkan engagement tertinggi\nresults.sort((a, b) => b.avgEngagement - a.avgEngagement);\n\n// Ambil top 10 jam terbaik\nconst top10 = results.slice(0, 10);\n\n// Tambahkan ranking\nconst rankedResults = top10.map((item, index) => ({\n  ranking: index + 1,\n  ...item,\n  rekomendasi: index < 3 ? '⭐ SANGAT DIREKOMENDASIKAN' : index < 5 ? '✅ DIREKOMENDASIKAN' : '👍 CUKUP BAIK'\n}));\n\n// Tambahkan timestamp analisis\nconst analysisDate = new Date().toLocaleString('id-ID', {\n  timeZone: 'Asia/Jakarta',\n  year: 'numeric',\n  month: '2-digit',\n  day: '2-digit',\n  hour: '2-digit',\n  minute: '2-digit'\n});\n\nconst finalResults = rankedResults.map(item => ({\n  ...item,\n  tanggalAnalisis: analysisDate,\n  totalDataDianalisis: processedCount\n}));\n\nconsole.log('Final results count:', finalResults.length);\n\nreturn finalResults.map(item => ({ json: item }));\n"
      },
      "type": "n8n-nodes-base.code",
      "typeVersion": 2,
      "position": [
        416,
        0
      ],
      "id": "1cf822bf-8f93-4c29-8e22-f089a78fd38a",
      "name": "analisis waktu terbaik"
    },
    {
      "parameters": {
        "operation": "clear",
        "documentId": {
          "__rl": true,
          "value": "1xeeRzunECQL_5tJvwgpWcpQ0Zcq0Wjkj4j9x0taU2Lo",
          "mode": "list",
          "cachedResultName": "Copy of Best Time to Post Data",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1xeeRzunECQL_5tJvwgpWcpQ0Zcq0Wjkj4j9x0taU2Lo/edit?usp=drivesdk"
        },
        "sheetName": {
          "__rl": true,
          "value": 723653925,
          "mode": "list",
          "cachedResultName": "Hasil Analisis",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1xeeRzunECQL_5tJvwgpWcpQ0Zcq0Wjkj4j9x0taU2Lo/edit#gid=723653925"
        }
      },
      "type": "n8n-nodes-base.googleSheets",
      "typeVersion": 4.7,
      "position": [
        624,
        0
      ],
      "id": "3196382b-8ad3-47db-9b89-3e0d8e632491",
      "name": "hapus hasil lama",
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
          "value": "1xeeRzunECQL_5tJvwgpWcpQ0Zcq0Wjkj4j9x0taU2Lo",
          "mode": "list",
          "cachedResultName": "Copy of Best Time to Post Data",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1xeeRzunECQL_5tJvwgpWcpQ0Zcq0Wjkj4j9x0taU2Lo/edit?usp=drivesdk"
        },
        "sheetName": {
          "__rl": true,
          "value": 723653925,
          "mode": "list",
          "cachedResultName": "Hasil Analisis",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1xeeRzunECQL_5tJvwgpWcpQ0Zcq0Wjkj4j9x0taU2Lo/edit#gid=723653925"
        },
        "columns": {
          "mappingMode": "defineBelow",
          "value": {},
          "matchingColumns": [],
          "schema": [
            {
              "id": "ranking",
              "displayName": "ranking",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "jam",
              "displayName": "jam",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "avgEngagement",
              "displayName": "avgEngagement",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "jumlahPost",
              "displayName": "jumlahPost",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "avgLikes",
              "displayName": "avgLikes",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "avgComments",
              "displayName": "avgComments",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "avgShares",
              "displayName": "avgShares",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "platformTerbanyak",
              "displayName": "platformTerbanyak",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "engagementScore",
              "displayName": "engagementScore",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "rekomendasi",
              "displayName": "rekomendasi",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "tanggalAnalisis",
              "displayName": "tanggalAnalisis",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "totalDataDianalisis",
              "displayName": "totalDataDianalisis",
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
        0
      ],
      "id": "f582b226-0b65-4905-a446-481b9cd55c4f",
      "name": "tulis hasil analisis",
      "credentials": {
        "googleSheetsOAuth2Api": {
          "id": "1i4CpejrRiWAa25G",
          "name": "Google Sheets account 3"
        }
      }
    },
    {
      "parameters": {
        "jsCode": "// Ambil hasil analisis dari input sebelumnya\nconst items = $input.all();\n\nif (!items || items.length === 0) {\n  return [{ json: { message: '❌ Tidak ada data untuk dikirim' } }];\n}\n\n// Ambil top 5 jam terbaik\nconst top5 = items.slice(0, 5);\nconst totalData = items[0].json.totalDataDianalisis || 'N/A';\nconst tanggalAnalisis = items[0].json.tanggalAnalisis || new Date().toLocaleString('id-ID');\n\n// Format pesan Telegram dengan emoji dan formatting\nlet message = `📊 *HASIL ANALISIS WAKTU POSTING TERBAIK*\\n`;\nmessage += `━━━━━━━━━━━━━━━━━━━━━━━━━━━━━\\n\\n`;\nmessage += `🏆 *TOP 5 JAM TERBAIK:*\\n\\n`;\n\ntop5.forEach((item, index) => {\n  const data = item.json;\n  const medal = index === 0 ? '🥇' : index === 1 ? '🥈' : index === 2 ? '🥉' : `${index + 1}.`;\n  \n  message += `${medal} *JAM ${data.jam}*\\n`;\n  message += `   📈 Avg Engagement: *${data.avgEngagement}*\\n`;\n  message += `   ❤️ Avg Likes: ${data.avgLikes}\\n`;\n  message += `   💬 Avg Comments: ${data.avgComments}\\n`;\n  message += `   🔄 Avg Shares: ${data.avgShares}\\n`;\n  message += `   📱 Platform: ${data.platformTerbanyak}\\n`;\n  message += `   📊 Total Post: ${data.jumlahPost} post\\n`;\n  message += `   ${data.rekomendasi}\\n\\n`;\n});\n\nmessage += `━━━━━━━━━━━━━━━━━━━━━━━━━━━━━\\n`;\nmessage += `💡 *REKOMENDASI:*\\n`;\nmessage += `Posting pada jam *${top5[0].json.jam}* memberikan engagement tertinggi dengan rata-rata *${top5[0].json.avgEngagement}* engagement!\\n\\n`;\n\nmessage += `📅 Analisis: ${tanggalAnalisis}\\n`;\nmessage += `📝 Total data: ${totalData} post\\n\\n`;\n\nmessage += `_Gunakan insight ini untuk optimasi strategi posting Anda!_ 🚀`;\n\nreturn [{ json: { \n  chatId: '',  // Akan diisi dari credential atau parameter\n  message: message,\n  parseMode: 'Markdown'\n} }];\n\n"
      },
      "type": "n8n-nodes-base.code",
      "typeVersion": 2,
      "position": [
        1040,
        0
      ],
      "id": "9798f291-4269-487b-9a4e-e5428698a432",
      "name": "format pesan telegram"
    }
  ],
  "connections": {
    "When clicking ‘Execute workflow’": {
      "main": [
        [
          {
            "node": "baca data posting",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "baca data posting": {
      "main": [
        [
          {
            "node": "analisis waktu terbaik",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "analisis waktu terbaik": {
      "main": [
        [
          {
            "node": "hapus hasil lama",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "hapus hasil lama": {
      "main": [
        [
          {
            "node": "tulis hasil analisis",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "tulis hasil analisis": {
      "main": [
        [
          {
            "node": "format pesan telegram",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "format pesan telegram": {
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
