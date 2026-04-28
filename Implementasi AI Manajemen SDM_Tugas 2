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
      "id": "acdd401b-667f-42c4-8266-7504219983ce",
      "name": "When clicking ‘Execute workflow’"
    },
    {
      "parameters": {
        "jsCode": "return [\n  {\n    json: {\n      id: 101,\n      candidate_name: \"Budi Santoso\",\n      email: \"budi.devops@email.test\",\n      position: \"Senior DevOps Engineer\",\n      claimed_skills: \"Kubernetes, Helm, Terraform\",\n      past_company_type: \"Agensi Digital Marketing (Non-Tech Product)\",\n      years_experience: 3,\n      interview_status: \"Scheduled\"\n    }\n  },\n  {\n    json: {\n      id: 102,\n      candidate_name: \"Siti Aminah\",\n      email: \"siti.backend@email.test\",\n      position: \"Backend Engineer\",\n      claimed_skills: \"Microservices, Kubernetes, GoLang\",\n      past_company_type: \"Bank Konvensional (Legacy System)\",\n      years_experience: 5,\n      interview_status: \"Scheduled\"\n    }\n  }\n];\n"
      },
      "type": "n8n-nodes-base.code",
      "typeVersion": 2,
      "position": [
        208,
        0
      ],
      "id": "a0c767bf-32b7-4122-9bef-5a04db986edf",
      "name": "Data Dummy"
    },
    {
      "parameters": {
        "options": {}
      },
      "type": "n8n-nodes-base.splitInBatches",
      "typeVersion": 3,
      "position": [
        416,
        0
      ],
      "id": "e1f44c22-bbba-4c34-a659-087ccf45a7ec",
      "name": "Loop Over Items"
    },
    {
      "parameters": {
        "jsCode": "for (const item of items) {\n  const candidate = item.json;\n  const role = candidate.position || \"Software Engineer\";\n  const skills = candidate.claimed_skills;\n  const background = candidate.past_company_type;\n  \n  const systemPrompt = `\n  Role: You are a Senior Technical Interviewer for a ${role} position. \n  Your goal is to validate the technical depth of a candidate named ${candidate.candidate_name}.\n  \n  CONTEXT:\n  The candidate claims expertise in: ${skills}.\n  However, their background is from: ${background}.\n  \n  TASK:\n  Generate 5 advanced technical interview questions (Studi Kasus) to verify if they truly understand the internal workings of the tech stack or just surface-level knowledge.\n  Focus on troubleshooting scenarios and architectural trade-offs.\n  \n  IMPORTANT: \n  - The questions must be challenging but professional.\n  - Provide the output in INDONESIAN language.\n  \n  OUTPUT FORMAT (Markdown):\n  1. **Topik**: [Nama Topik]\n     - **Pertanyaan**: [Studi Kasus Spesifik]\n     - **Ekspektasi Jawaban Senior**: [Poin Kunci]\n  `;\n\n  item.json.llm_prompt = systemPrompt;\n}\n\nreturn items;\n"
      },
      "type": "n8n-nodes-base.code",
      "typeVersion": 2,
      "position": [
        640,
        16
      ],
      "id": "6a971a15-901b-4a49-bf80-42ad11a1e979",
      "name": "Prompt Bullder"
    },
    {
      "parameters": {
        "promptType": "define",
        "text": "={{ $json.llm_prompt }}",
        "batching": {}
      },
      "type": "@n8n/n8n-nodes-langchain.chainLlm",
      "typeVersion": 1.9,
      "position": [
        848,
        16
      ],
      "id": "86a31097-ec7d-46a4-b58d-2634a64d709c",
      "name": "Basic LLM Chain"
    },
    {
      "parameters": {
        "chatId": "1535237765",
        "text": "=Nama kandidat: {{ $json('Data Dummy').item.json.candidate_name }}\n{{ $json.text }}",
        "additionalFields": {}
      },
      "type": "n8n-nodes-base.telegram",
      "typeVersion": 1.2,
      "position": [
        1184,
        16
      ],
      "id": "c99b3414-a887-498d-bdbf-9380c069b288",
      "name": "Send a text message",
      "webhookId": "420cd9e8-c0cb-4dcf-8c2c-2c5ea23c2a75",
      "credentials": {
        "telegramApi": {
          "id": "UeW4rIKFaGuH61DK",
          "name": "bot renjeun"
        }
      }
    },
    {
      "parameters": {
        "jsCode": "const aiQuestion = items[0].json.text; \n\n\nconst candidateName = $('Loop Over Items').item.json.candidate_name;\n\nlet mockAnswer = \"\";\n\nif (candidateName.includes(\"Budi\")) {\n  mockAnswer = \"Untuk masalah CrashLoopBackOff, saya akan cek logs pod pakai kubectl logs, lalu describe pod untuk lihat events. Biasanya karena configmap salah atau app panic saat startup.\";\n} else {\n  mockAnswer = \"Saya biasanya restart servernya pak. Kalau masih error saya install ulang Kubernetesnya.\";\n}\n\nreturn [\n  {\n    json: {\n      question: aiQuestion,\n      candidate_answer: mockAnswer,\n      candidate_name: candidateName\n    }\n  }\n];"
      },
      "type": "n8n-nodes-base.code",
      "typeVersion": 2,
      "position": [
        592,
        368
      ],
      "id": "1395075f-173c-4976-9d30-7933bb502852",
      "name": "Mock Jawaban"
    },
    {
      "parameters": {
        "jsCode": "const data = items[0].json;\n\nconst prompt = `\nROLE: You are a Senior Hiring Manager.\nTASK: Evaluate the candidate's answer based on the technical question provided.\n\nDATA:\n- Candidate Name: ${data.candidate_name}\n- Question Given: \"${data.question.substring(0, 200)}...\" (Truncated for brevity)\n- Candidate Answer: \"${data.candidate_answer}\"\n\nINSTRUCTION:\nGive a score (0-100) and a brief critique.\n- If the answer shows deep troubleshooting steps (logs, events, root cause), give HIGH score.\n- If the answer is generic (restart server, reinstall), give LOW score (Red Flag).\n\nOUTPUT FORMAT (Indonesian):\n**Penilaian untuk ${data.candidate_name}**\n--------------------------\n🎯 **Skor:** [0-100]\n💡 **Analisa:** [Penjelasan singkat 1 kalimat]\n🚫 **Keputusan:** [LOLOS / GAGAL]\n`;\n\nreturn [\n  {\n    json: {\n      eval_prompt: prompt\n    }\n  }\n];\n"
      },
      "type": "n8n-nodes-base.code",
      "typeVersion": 2,
      "position": [
        800,
        368
      ],
      "id": "4eb0a2fa-a22d-4142-b6a4-e5d87d8c6d9a",
      "name": "Evaluator"
    },
    {
      "parameters": {
        "promptType": "define",
        "text": "={{ $json.eval_prompt }}",
        "batching": {}
      },
      "type": "@n8n/n8n-nodes-langchain.chainLlm",
      "typeVersion": 1.9,
      "position": [
        1008,
        368
      ],
      "id": "188209aa-057b-4f61-b05d-245064813b80",
      "name": "Basic LLM Chain1"
    },
    {
      "parameters": {
        "chatId": "1535237765",
        "text": "=Nama kandidat: {{ $json('Data Dummy').item.json.candidate_name }}\n{{ $json.text }}",
        "additionalFields": {}
      },
      "type": "n8n-nodes-base.telegram",
      "typeVersion": 1.2,
      "position": [
        1328,
        368
      ],
      "id": "149396da-16d0-421d-a533-851e24e45805",
      "name": "Send a text message1",
      "webhookId": "420cd9e8-c0cb-4dcf-8c2c-2c5ea23c2a75",
      "credentials": {
        "telegramApi": {
          "id": "UeW4rIKFaGuH61DK",
          "name": "bot renjeun"
        }
      }
    },
    {
      "parameters": {
        "model": "liquid/lfm-2.5-1.2b-thinking:free",
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.lmChatOpenRouter",
      "typeVersion": 1,
      "position": [
        784,
        224
      ],
      "id": "b55930b9-c8c1-4d73-9038-44241618865d",
      "name": "OpenRouter Chat Model",
      "credentials": {
        "openRouterApi": {
          "id": "690Ovy8cCHBHAqHt",
          "name": "awa"
        }
      }
    }
  ],
  "connections": {
    "When clicking ‘Execute workflow’": {
      "main": [
        [
          {
            "node": "Data Dummy",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Data Dummy": {
      "main": [
        [
          {
            "node": "Loop Over Items",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Loop Over Items": {
      "main": [
        [],
        [
          {
            "node": "Prompt Bullder",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Prompt Bullder": {
      "main": [
        [
          {
            "node": "Basic LLM Chain",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Basic LLM Chain": {
      "main": [
        [
          {
            "node": "Loop Over Items",
            "type": "main",
            "index": 0
          },
          {
            "node": "Send a text message",
            "type": "main",
            "index": 0
          },
          {
            "node": "Mock Jawaban",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Mock Jawaban": {
      "main": [
        [
          {
            "node": "Evaluator",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Evaluator": {
      "main": [
        [
          {
            "node": "Basic LLM Chain1",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Basic LLM Chain1": {
      "main": [
        [
          {
            "node": "Send a text message1",
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
            "node": "Basic LLM Chain",
            "type": "ai_languageModel",
            "index": 0
          },
          {
            "node": "Basic LLM Chain1",
            "type": "ai_languageModel",
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
