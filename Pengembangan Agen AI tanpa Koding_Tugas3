{
  "nodes": [
    {
      "parameters": {
        "public": true,
        "initialMessages": "halooo\n",
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.chatTrigger",
      "typeVersion": 1.4,
      "position": [
        0,
        0
      ],
      "id": "a307a118-8f58-456f-938c-8c7957283319",
      "name": "When chat message received",
      "webhookId": "f2326c7a-1639-4c31-b35d-98f42b7c7756"
    },
    {
      "parameters": {
        "options": {
          "systemMessage": "Anda adalah asisten virtual resmi dari NF Academy yang bertugas memberikan informasi lengkap dan akurat mengenai berbagai program pelatihan yang tersedia kepada calon peserta. Dalam menjalankan tugas ini, Anda harus selalu bersikap ramah, profesional, dan solutif dengan menggunakan data yang bersumber dari Google Sheets melalui tool yang telah terintegrasi untuk menjawab setiap pertanyaan mengenai jenis program, nama kursus, deskripsi materi, hingga rincian biaya pelatihan. Jika pengguna menanyakan tentang program Bootcamp, Anda harus menjelaskan bahwa biaya rata-ratanya adalah 15.000.000 dengan pilihan bidang seperti Digital Marketing, Network Engineering, Web Development, Mobile Programming, Data Science, hingga DevOps. Sementara itu, jika pengguna menanyakan program Skill Up, Anda perlu merinci materi spesifik seperti Video Editing, Python, PHP, Laravel, hingga administrasi sistem Linux dengan rentang harga mulai dari 1.700.000 sampai 3.500.000 sesuai dengan data yang tertera pada tabel. Pastikan setiap jawaban yang diberikan disampaikan dalam bahasa Indonesia yang formal namun tetap nyaman dibaca, serta jangan lupa untuk selalu memberikan dorongan kepada pengguna agar segera melakukan pendaftaran apabila mereka menyatakan ketertarikan pada salah satu program pelatihan tersebut. Apabila ada pertanyaan mengenai informasi yang tidak tercantum di dalam data Google Sheets, sampaikan permohonan maaf dengan sopan dan informasikan bahwa pertanyaan tersebut akan segera diteruskan kepada tim admin untuk ditindaklanjuti lebih lanjut."
        }
      },
      "type": "@n8n/n8n-nodes-langchain.agent",
      "typeVersion": 3.1,
      "position": [
        208,
        0
      ],
      "id": "a0772153-ebbf-4665-ac83-5b4a03075703",
      "name": "AI Agent"
    },
    {
      "parameters": {
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.lmChatGoogleGemini",
      "typeVersion": 1,
      "position": [
        80,
        208
      ],
      "id": "5a8fcfc2-14b2-4957-a710-a180df26f1ba",
      "name": "Google Gemini Chat Model",
      "credentials": {
        "googlePalmApi": {
          "id": "qA1uVlz3z2Seif8h",
          "name": "Google Gemini(PaLM) Api account 3"
        }
      }
    },
    {
      "parameters": {},
      "type": "@n8n/n8n-nodes-langchain.memoryBufferWindow",
      "typeVersion": 1.3,
      "position": [
        224,
        208
      ],
      "id": "ff436782-5d53-46a4-b154-79bddc31d732",
      "name": "Simple Memory"
    },
    {
      "parameters": {
        "documentId": {
          "__rl": true,
          "value": "1hIaXz3KVJl6nmRG7Pz7UTszXWVMlFsrSvPZpBFzXhIE",
          "mode": "list",
          "cachedResultName": "n8n 1",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1hIaXz3KVJl6nmRG7Pz7UTszXWVMlFsrSvPZpBFzXhIE/edit?usp=drivesdk"
        },
        "sheetName": {
          "__rl": true,
          "value": "gid=0",
          "mode": "list",
          "cachedResultName": "Sheet1",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1hIaXz3KVJl6nmRG7Pz7UTszXWVMlFsrSvPZpBFzXhIE/edit#gid=0"
        },
        "options": {}
      },
      "type": "n8n-nodes-base.googleSheetsTool",
      "typeVersion": 4.7,
      "position": [
        368,
        208
      ],
      "id": "bd07812a-2f05-489c-b38f-2d9ac63a1ea7",
      "name": "Get row(s) in sheet in Google Sheets",
      "credentials": {
        "googleSheetsOAuth2Api": {
          "id": "1i4CpejrRiWAa25G",
          "name": "Google Sheets account 3"
        }
      }
    }
  ],
  "connections": {
    "When chat message received": {
      "main": [
        [
          {
            "node": "AI Agent",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Google Gemini Chat Model": {
      "ai_languageModel": [
        [
          {
            "node": "AI Agent",
            "type": "ai_languageModel",
            "index": 0
          }
        ]
      ]
    },
    "Simple Memory": {
      "ai_memory": [
        [
          {
            "node": "AI Agent",
            "type": "ai_memory",
            "index": 0
          }
        ]
      ]
    },
    "Get row(s) in sheet in Google Sheets": {
      "ai_tool": [
        [
          {
            "node": "AI Agent",
            "type": "ai_tool",
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
