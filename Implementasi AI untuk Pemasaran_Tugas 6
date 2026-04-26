{
  "nodes": [
    {
      "parameters": {
        "updates": [
          "message"
        ],
        "additionalFields": {}
      },
      "type": "n8n-nodes-base.telegramTrigger",
      "typeVersion": 1.2,
      "position": [
        -1728,
        896
      ],
      "id": "24df00f9-d39d-42bc-85d5-07a20e4ddf2f",
      "name": "Telegram Trigger",
      "webhookId": "56d66f41-ed1e-418d-8115-70c0c95a3e5d",
      "credentials": {
        "telegramApi": {
          "id": "UeW4rIKFaGuH61DK",
          "name": "bot renjeun"
        }
      }
    },
    {
      "parameters": {
        "chatId": "={{ $node[\"Telegram Trigger\"].json.message.chat.id }}",
        "text": "Harap ketik/start untuk mulai.",
        "additionalFields": {}
      },
      "type": "n8n-nodes-base.telegram",
      "typeVersion": 1.2,
      "position": [
        -1376,
        1216
      ],
      "id": "b9cb3462-860d-4ec1-a7e2-5d754791fdb1",
      "name": "Respon Cepat",
      "webhookId": "1a6e2660-3cca-4d0d-9856-7a0ce6e2cf35",
      "credentials": {
        "telegramApi": {
          "id": "UeW4rIKFaGuH61DK",
          "name": "bot renjeun"
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
                  "caseSensitive": true,
                  "leftValue": "",
                  "typeValidation": "strict",
                  "version": 3
                },
                "conditions": [
                  {
                    "leftValue": "={{ $node[\"Telegram Trigger\"].json.message.text }}",
                    "rightValue": "/start",
                    "operator": {
                      "type": "string",
                      "operation": "contains"
                    },
                    "id": "a7ea765b-87ff-47d0-b043-02e9a0ea0d45"
                  }
                ],
                "combinator": "and"
              }
            },
            {
              "conditions": {
                "options": {
                  "caseSensitive": true,
                  "leftValue": "",
                  "typeValidation": "strict",
                  "version": 3
                },
                "conditions": [
                  {
                    "id": "3767999a-aa45-4d3a-a854-c2d5cd2547a9",
                    "leftValue": "={{ $json.message.text }}",
                    "rightValue": "title",
                    "operator": {
                      "type": "string",
                      "operation": "contains"
                    }
                  }
                ],
                "combinator": "and"
              }
            },
            {
              "conditions": {
                "options": {
                  "caseSensitive": true,
                  "leftValue": "",
                  "typeValidation": "strict",
                  "version": 3
                },
                "conditions": [
                  {
                    "id": "4f349a97-86b0-4501-9af7-0eb7e7e79ff8",
                    "leftValue": "={{ $json.message.caption || $json.message.text }}",
                    "rightValue": "video",
                    "operator": {
                      "type": "string",
                      "operation": "contains"
                    }
                  }
                ],
                "combinator": "and"
              }
            },
            {
              "conditions": {
                "options": {
                  "caseSensitive": true,
                  "leftValue": "",
                  "typeValidation": "strict",
                  "version": 3
                },
                "conditions": [
                  {
                    "id": "4dac19a8-e647-4ec5-9f66-60c1403cb0a4",
                    "leftValue": "={{ $node[\"Telegram Trigger\"].json.message.text }}",
                    "rightValue": "respon cepat",
                    "operator": {
                      "type": "string",
                      "operation": "equals",
                      "name": "filter.operator.equals"
                    }
                  }
                ],
                "combinator": "and"
              }
            }
          ]
        },
        "options": {}
      },
      "type": "n8n-nodes-base.switch",
      "typeVersion": 3.4,
      "position": [
        -1488,
        864
      ],
      "id": "087a78a4-aa73-40f1-bb81-cb4621145842",
      "name": "Switch"
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
              "id": "9d482b83-0134-4846-8acd-87ac5bc5d2e1",
              "leftValue": "={{ $node[\"Telegram Trigger\"].json.message.text }}",
              "rightValue": "/start",
              "operator": {
                "type": "string",
                "operation": "contains"
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
        -1072,
        592
      ],
      "id": "13d312d3-7f3e-46a0-b667-015edd2ae3c7",
      "name": "If"
    },
    {
      "parameters": {
        "operation": "binaryToPropery",
        "options": {}
      },
      "type": "n8n-nodes-base.extractFromFile",
      "typeVersion": 1.1,
      "position": [
        -864,
        1216
      ],
      "id": "9cbe4774-e221-4685-a3d9-e7ba46e2b386",
      "name": "Extract from File"
    },
    {
      "parameters": {
        "jsCode": "// Gunakan ini di node \"Code in JavaScript\"\nconst items = $input.all();\nfor (let item of items) {\n  if (item.json.data) {\n    item.binary = {\n      data: {\n        data: item.json.data, // assuming base64 string\n        fileName: 'input_image.jpg',\n        mimeType: 'image/jpeg'\n      }\n    };\n  }\n}\nreturn items;"
      },
      "type": "n8n-nodes-base.code",
      "typeVersion": 2,
      "position": [
        -656,
        1216
      ],
      "id": "0e704fdc-dd0a-41af-81dc-f9b826780773",
      "name": "Code in JavaScript"
    },
    {
      "parameters": {
        "resource": "image",
        "operation": "analyze",
        "modelId": {
          "__rl": true,
          "value": "models/gemini-2.5-flash",
          "mode": "list",
          "cachedResultName": "models/gemini-2.5-flash"
        },
        "text": "Analyze the image and generate a detailed, cinematic video prompt suitable for Google VEO-3.1. Include:\n- Subject and action (e.g., \"a cat jumping on a sofa\")\n- Setting and background\n- Time of day, lighting, mood\n- Camera movement (e.g., slow zoom, tracking shot)\n- Visual style (e.g., photorealistic, cartoon, cinematic)\n\nKeep it concise (1–2 sentences). Output ONLY the prompt text, no explanation.\n",
        "inputType": "binary",
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.googleGemini",
      "typeVersion": 1.1,
      "position": [
        -448,
        1216
      ],
      "id": "d582ec19-87ba-4ff7-8fce-b3e5197fbf7d",
      "name": "Analyze an image",
      "credentials": {
        "googlePalmApi": {
          "id": "VN9VIMxifDECoNRe",
          "name": "n8n renjun"
        }
      }
    },
    {
      "parameters": {
        "operation": "sendVideo",
        "chatId": "={{ $node[\"Telegram Trigger\"].json.message.chat.id }}",
        "binaryData": true,
        "additionalFields": {}
      },
      "type": "n8n-nodes-base.telegram",
      "typeVersion": 1.2,
      "position": [
        160,
        1216
      ],
      "id": "b76e905e-99e4-4236-9fde-764ccb1ee8f6",
      "name": "Send a video",
      "webhookId": "5dcbf2ae-a09e-4c6c-b547-0889695ddf28",
      "credentials": {
        "telegramApi": {
          "id": "UeW4rIKFaGuH61DK",
          "name": "bot renjeun"
        }
      }
    },
    {
      "parameters": {
        "operation": "sendPhoto",
        "chatId": "={{ $node[\"Telegram Trigger\"].json.message.chat.id }}",
        "binaryData": true,
        "additionalFields": {}
      },
      "type": "n8n-nodes-base.telegram",
      "typeVersion": 1.2,
      "position": [
        -384,
        880
      ],
      "id": "9346b1ca-b7c8-4d16-a2fa-21e01265e904",
      "name": "Send a photo message",
      "webhookId": "f4c474bd-837e-4d50-8698-c36f2c4fd7e8",
      "credentials": {
        "telegramApi": {
          "id": "UeW4rIKFaGuH61DK",
          "name": "bot renjeun"
        }
      }
    },
    {
      "parameters": {
        "chatId": "={{ $node[\"Telegram Trigger\"].json.message.chat.id }}",
        "text": "Maaf, perintah tidak dikenali. 🙏 \\n\\nSilakan ketik:\\n- /start untuk memulai\\n- title untuk membuat rencana konten\\n- video (sambil kirim gambar) untuk generate video",
        "additionalFields": {}
      },
      "type": "n8n-nodes-base.telegram",
      "typeVersion": 1.2,
      "position": [
        -864,
        304
      ],
      "id": "8821b0ec-d2a7-4b3a-b614-07e965ffc9da",
      "name": "Send a text message",
      "webhookId": "7b65de16-5159-4ca6-be4d-5fc1dd4f60c1",
      "credentials": {
        "telegramApi": {
          "id": "UeW4rIKFaGuH61DK",
          "name": "bot renjeun"
        }
      }
    },
    {
      "parameters": {
        "assignments": {
          "assignments": [
            {
              "id": "b746c33f-5dc7-4bf7-bfe8-fb0e935ca19c",
              "name": "tanggal",
              "value": "{{ $json['Readable date'] }}",
              "type": "string"
            },
            {
              "id": "9827fbfa-a019-4bf4-bd84-fb33c955d423",
              "name": "tema",
              "value": "Teknologi & Produktivitas",
              "type": "string"
            },
            {
              "id": "0adbc742-8b6d-473d-965c-94cd00754a3e",
              "name": "waktu",
              "value": "={{ $json['Readable time'] }}",
              "type": "string"
            }
          ]
        },
        "options": {}
      },
      "type": "n8n-nodes-base.set",
      "typeVersion": 3.4,
      "position": [
        -672,
        512
      ],
      "id": "f05118a9-172f-456e-8d86-40722932cc79",
      "name": "Edit Fields"
    },
    {
      "parameters": {
        "promptType": "define",
        "text": "=Buat rencana konten harian untuk {{ $json.tanggal }} dengan tema  {{ $json.tema }} \n\nSaya mau Anda buatnya dalam bentuk nomor atau point.\n",
        "hasOutputParser": true,
        "batching": {}
      },
      "type": "@n8n/n8n-nodes-langchain.chainLlm",
      "typeVersion": 1.9,
      "position": [
        -352,
        496
      ],
      "id": "cd22a92f-6993-479e-b48e-46cfb8fef57c",
      "name": "Basic LLM Chain"
    },
    {
      "parameters": {
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.lmChatGoogleGemini",
      "typeVersion": 1,
      "position": [
        -352,
        320
      ],
      "id": "abf4fb21-5d26-4766-a0c2-e712c0ed1ce8",
      "name": "Google Gemini Chat Model",
      "credentials": {
        "googlePalmApi": {
          "id": "qA1uVlz3z2Seif8h",
          "name": "Google Gemini(PaLM) Api account 3"
        }
      }
    },
    {
      "parameters": {
        "numberInputs": 4
      },
      "type": "n8n-nodes-base.merge",
      "typeVersion": 3.2,
      "position": [
        256,
        416
      ],
      "id": "2a389b56-c488-4d44-9690-82c6ff7bf60f",
      "name": "Merge"
    },
    {
      "parameters": {
        "assignments": {
          "assignments": [
            {
              "id": "70455a99-8c23-4de9-87fe-db3ea359dd41",
              "name": "time_slot",
              "value": "={{ $json.output[0].time_slot }}",
              "type": "string"
            },
            {
              "id": "cdb2677f-7947-43af-9490-7bbb70546272",
              "name": "title",
              "value": "={{ $json.output[0].title }}",
              "type": "string"
            },
            {
              "id": "87653dba-2291-48e2-970d-23eae07123f9",
              "name": "platfrom",
              "value": "={{ $json.output[0].platfroms }}",
              "type": "string"
            },
            {
              "id": "e83a23ee-41a7-41fb-984e-7a1623109cca",
              "name": "focus",
              "value": "={{ $json.output[0].focus }}",
              "type": "string"
            },
            {
              "id": "a58b4aaf-0833-467a-a27c-b426559ddfbd",
              "name": "ide",
              "value": "={{ $json.output[0].ideas }}",
              "type": "string"
            }
          ]
        },
        "options": {}
      },
      "type": "n8n-nodes-base.set",
      "typeVersion": 3.4,
      "position": [
        0,
        0
      ],
      "id": "b0e72f7d-ffe2-4a04-957c-70a1893a6051",
      "name": "Edit Fields1"
    },
    {
      "parameters": {
        "chatId": "1535237765",
        "text": "Title: {{ $json.title \n\n \"Tidak ada judul\" }} Platform: {{ $json.platfrom \n\n \"Tidak ada platform\" }} Ide: {{ $json.ide \n\n \"Tidak ada ide\" }}",
        "additionalFields": {}
      },
      "type": "n8n-nodes-base.telegram",
      "typeVersion": 1.2,
      "position": [
        464,
        448
      ],
      "id": "1073a6f0-f8e5-4454-80e6-4303f1bc5949",
      "name": "Send a text message1",
      "webhookId": "7f986881-d5d7-44b1-b4c8-4d2d727e49ac",
      "credentials": {
        "telegramApi": {
          "id": "UeW4rIKFaGuH61DK",
          "name": "bot renjeun"
        }
      }
    },
    {
      "parameters": {
        "jsonSchemaExample": "[\n  {\n    \"time_slot\": \"\",\n    \"title\": \"\",\n    \"platforms\": [],\n    \"focus\": \"\",\n    \"ideas\": []\n  }\n]\n"
      },
      "type": "@n8n/n8n-nodes-langchain.outputParserStructured",
      "typeVersion": 1.3,
      "position": [
        -224,
        304
      ],
      "id": "30df41de-4619-40b6-8a5b-412d5a85d21d",
      "name": "Structured Output Parser"
    },
    {
      "parameters": {
        "assignments": {
          "assignments": [
            {
              "id": "70455a99-8c23-4de9-87fe-db3ea359dd41",
              "name": "time_slot",
              "value": "={{ $json.output[0].time_slot }}",
              "type": "string"
            },
            {
              "id": "cdb2677f-7947-43af-9490-7bbb70546272",
              "name": "title",
              "value": "={{ $json.output[0].title }}",
              "type": "string"
            },
            {
              "id": "87653dba-2291-48e2-970d-23eae07123f9",
              "name": "platfrom",
              "value": "={{ $json.output[0].platfroms }}",
              "type": "string"
            },
            {
              "id": "e83a23ee-41a7-41fb-984e-7a1623109cca",
              "name": "focus",
              "value": "={{ $json.output[0].focus }}",
              "type": "string"
            },
            {
              "id": "a58b4aaf-0833-467a-a27c-b426559ddfbd",
              "name": "ide",
              "value": "={{ $json.output[0].ideas }}",
              "type": "string"
            }
          ]
        },
        "options": {}
      },
      "type": "n8n-nodes-base.set",
      "typeVersion": 3.4,
      "position": [
        0,
        176
      ],
      "id": "a2f3d757-ed4a-49e3-8495-82214410b386",
      "name": "Edit Fields2"
    },
    {
      "parameters": {
        "assignments": {
          "assignments": [
            {
              "id": "70455a99-8c23-4de9-87fe-db3ea359dd41",
              "name": "time_slot",
              "value": "={{ $json.output[0].time_slot }}",
              "type": "string"
            },
            {
              "id": "cdb2677f-7947-43af-9490-7bbb70546272",
              "name": "title",
              "value": "={{ $json.output[0].title }}",
              "type": "string"
            },
            {
              "id": "87653dba-2291-48e2-970d-23eae07123f9",
              "name": "platfrom",
              "value": "={{ $json.output[0].platfroms }}",
              "type": "string"
            },
            {
              "id": "e83a23ee-41a7-41fb-984e-7a1623109cca",
              "name": "focus",
              "value": "={{ $json.output[0].focus }}",
              "type": "string"
            },
            {
              "id": "a58b4aaf-0833-467a-a27c-b426559ddfbd",
              "name": "ide",
              "value": "={{ $json.output[0].ideas }}",
              "type": "string"
            }
          ]
        },
        "options": {}
      },
      "type": "n8n-nodes-base.set",
      "typeVersion": 3.4,
      "position": [
        0,
        336
      ],
      "id": "618f8f74-b879-438b-8dd6-3480c7b272ad",
      "name": "Edit Fields3"
    },
    {
      "parameters": {
        "assignments": {
          "assignments": [
            {
              "id": "70455a99-8c23-4de9-87fe-db3ea359dd41",
              "name": "time_slot",
              "value": "={{ $json.output[0].time_slot }}",
              "type": "string"
            },
            {
              "id": "cdb2677f-7947-43af-9490-7bbb70546272",
              "name": "title",
              "value": "={{ $json.output[0].title }}",
              "type": "string"
            },
            {
              "id": "87653dba-2291-48e2-970d-23eae07123f9",
              "name": "platfrom",
              "value": "={{ $json.output[0].platfroms }}",
              "type": "string"
            },
            {
              "id": "e83a23ee-41a7-41fb-984e-7a1623109cca",
              "name": "focus",
              "value": "={{ $json.output[0].focus }}",
              "type": "string"
            },
            {
              "id": "a58b4aaf-0833-467a-a27c-b426559ddfbd",
              "name": "ide",
              "value": "={{ $json.output[0].ideas }}",
              "type": "string"
            }
          ]
        },
        "options": {}
      },
      "type": "n8n-nodes-base.set",
      "typeVersion": 3.4,
      "position": [
        0,
        496
      ],
      "id": "edf62c85-6bc0-403c-aab3-5fcc295e83f3",
      "name": "Edit Fields4"
    },
    {
      "parameters": {
        "resource": "video",
        "modelId": {
          "__rl": true,
          "value": "models/veo-3.1-lite-generate-preview",
          "mode": "list",
          "cachedResultName": "models/veo-3.1-lite-generate-preview"
        },
        "prompt": "{{ $json.content.parts[0].text }}",
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.googleGemini",
      "typeVersion": 1.1,
      "position": [
        -48,
        1216
      ],
      "id": "ed5cd739-a936-4913-99d5-15856077354f",
      "name": "Generate a video",
      "credentials": {
        "googlePalmApi": {
          "id": "VN9VIMxifDECoNRe",
          "name": "n8n renjun"
        }
      }
    },
    {
      "parameters": {
        "assignments": {
          "assignments": [
            {
              "id": "d97f7f26-2e20-4a1e-8d64-8a20dcfe3d32",
              "name": "prompt",
              "value": "={{ $json.message.text.toLowerCase().replace('title', '').trim() }}",
              "type": "string"
            }
          ]
        },
        "options": {}
      },
      "type": "n8n-nodes-base.set",
      "typeVersion": 3.4,
      "position": [
        -1040,
        880
      ],
      "id": "75515b37-c362-44b7-9e33-d61205d58e82",
      "name": "Edit Fields5"
    },
    {
      "parameters": {
        "mode": "raw",
        "jsonOutput": "{\n  \"model\": \"grok-2-vision-1212\", \n  \"prompt\": \"{{ $json.prompt }}\",\n  \"aspect_ratio\": \"1:1\"\n}",
        "options": {}
      },
      "type": "n8n-nodes-base.set",
      "typeVersion": 3.4,
      "position": [
        -832,
        880
      ],
      "id": "bb140211-6f72-4cec-b8f7-36d204ca0f91",
      "name": "Edit Fields6"
    },
    {
      "parameters": {
        "method": "POST",
        "url": "https://image.pollinations.ai/prompt/{{ encodeURIComponent($json.prompt) }}?seed={{ Math.floor(Math.random() * 1000000) }}",
        "sendBody": true,
        "bodyParameters": {
          "parameters": [
            {}
          ]
        },
        "options": {
          "response": {
            "response": {
              "responseFormat": "file"
            }
          }
        }
      },
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 4.4,
      "position": [
        -624,
        880
      ],
      "id": "335d3972-d5b0-4397-ae2a-f8d2ff5b9738",
      "name": "HTTP Request"
    },
    {
      "parameters": {
        "resource": "file",
        "fileId": "={{ $node[\"Telegram Trigger\"].json.message.photo.reverse()[0].file_id }}",
        "additionalFields": {}
      },
      "type": "n8n-nodes-base.telegram",
      "typeVersion": 1.2,
      "position": [
        -1136,
        1216
      ],
      "id": "77db3b36-d60b-4ef2-82dd-00ba682a45ca",
      "name": "Get a file",
      "webhookId": "6cc04bb3-7e33-4ea1-a057-dbc982b58f69",
      "credentials": {
        "telegramApi": {
          "id": "UeW4rIKFaGuH61DK",
          "name": "bot renjeun"
        }
      }
    },
    {
      "parameters": {
        "amount": 10,
        "unit": "minutes"
      },
      "type": "n8n-nodes-base.wait",
      "typeVersion": 1.1,
      "position": [
        -240,
        1216
      ],
      "id": "438c91f1-e246-4835-bcc0-e02df652a203",
      "name": "Wait",
      "webhookId": "3ba9e5e1-76b7-4436-84ed-f92d94ee2b73"
    }
  ],
  "connections": {
    "Telegram Trigger": {
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
            "node": "If",
            "type": "main",
            "index": 0
          }
        ],
        [
          {
            "node": "Edit Fields5",
            "type": "main",
            "index": 0
          }
        ],
        [
          {
            "node": "Get a file",
            "type": "main",
            "index": 0
          }
        ],
        [
          {
            "node": "Respon Cepat",
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
            "node": "Edit Fields",
            "type": "main",
            "index": 0
          }
        ],
        [
          {
            "node": "Send a text message",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Extract from File": {
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
    "Code in JavaScript": {
      "main": [
        [
          {
            "node": "Analyze an image",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Analyze an image": {
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
    "Edit Fields": {
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
            "node": "Edit Fields1",
            "type": "main",
            "index": 0
          },
          {
            "node": "Edit Fields2",
            "type": "main",
            "index": 0
          },
          {
            "node": "Edit Fields3",
            "type": "main",
            "index": 0
          },
          {
            "node": "Edit Fields4",
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
            "node": "Basic LLM Chain",
            "type": "ai_languageModel",
            "index": 0
          }
        ]
      ]
    },
    "Merge": {
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
    "Edit Fields1": {
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
    "Structured Output Parser": {
      "ai_outputParser": [
        [
          {
            "node": "Basic LLM Chain",
            "type": "ai_outputParser",
            "index": 0
          }
        ]
      ]
    },
    "Edit Fields2": {
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
    "Edit Fields3": {
      "main": [
        [
          {
            "node": "Merge",
            "type": "main",
            "index": 2
          }
        ]
      ]
    },
    "Edit Fields4": {
      "main": [
        [
          {
            "node": "Merge",
            "type": "main",
            "index": 3
          }
        ]
      ]
    },
    "Generate a video": {
      "main": [
        [
          {
            "node": "Send a video",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Edit Fields5": {
      "main": [
        [
          {
            "node": "Edit Fields6",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Edit Fields6": {
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
    },
    "Get a file": {
      "main": [
        [
          {
            "node": "Extract from File",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Wait": {
      "main": [
        [
          {
            "node": "Generate a video",
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
