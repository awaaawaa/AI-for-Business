{
  "nodes": [
    {
      "parameters": {
        "updates": [
          "message",
          "callback_query"
        ],
        "additionalFields": {}
      },
      "type": "n8n-nodes-base.telegramTrigger",
      "typeVersion": 1.2,
      "position": [
        -1376,
        304
      ],
      "id": "560c38d2-2473-42f9-9231-6bc5e847324a",
      "name": "Telegram Trigger",
      "webhookId": "db0e2a73-e407-44fd-b4b7-799fcda60e54",
      "credentials": {
        "telegramApi": {
          "id": "n7cxOzcieENzevJa",
          "name": "mark lee"
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
                  "typeValidation": "loose",
                  "version": 3
                },
                "conditions": [
                  {
                    "leftValue": "={{ $json.message.text }}",
                    "rightValue": "/start",
                    "operator": {
                      "type": "string",
                      "operation": "equals"
                    },
                    "id": "0ccd447d-bffd-4fc3-b676-10cb4479588f"
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
                  "typeValidation": "loose",
                  "version": 3
                },
                "conditions": [
                  {
                    "id": "5a5af842-395f-476c-8f1a-5cdb58acee5a",
                    "leftValue": "={{ $json.callback_query.data }}",
                    "rightValue": "is not empty",
                    "operator": {
                      "type": "string",
                      "operation": "notEquals"
                    }
                  }
                ],
                "combinator": "and"
              }
            }
          ]
        },
        "looseTypeValidation": true,
        "options": {}
      },
      "type": "n8n-nodes-base.switch",
      "typeVersion": 3.4,
      "position": [
        -1120,
        304
      ],
      "id": "c1442e54-e941-440b-b4ce-a1181ccc6050",
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
              "id": "01785647-d094-4431-9518-6d8f815490d2",
              "leftValue": "={{ $json.message.text }}",
              "rightValue": "/start",
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
        -896,
        288
      ],
      "id": "eaa82ff5-6991-41c5-b0de-3e3afd95d38b",
      "name": "If"
    },
    {
      "parameters": {
        "chatId": "={{ $('Telegram Trigger').item.json.message.chat.id }}",
        "text": "Selamat datang di asisten SOP Mark lee!! Anda bisa bertanya menguunakan menu dibawah ini.",
        "replyMarkup": "inlineKeyboard",
        "inlineKeyboard": {
          "rows": [
            {
              "row": {
                "buttons": [
                  {
                    "text": "Prosedur Reimbursement",
                    "additionalFields": {
                      "callback_data": "reimbursement"
                    }
                  }
                ]
              }
            },
            {
              "row": {
                "buttons": [
                  {
                    "text": "Prosedur Cuti",
                    "additionalFields": {
                      "callback_data": "cuti"
                    }
                  }
                ]
              }
            },
            {
              "row": {
                "buttons": [
                  {
                    "text": "Aturan Lembur",
                    "additionalFields": {
                      "callback_data": "lembur"
                    }
                  }
                ]
              }
            },
            {
              "row": {
                "buttons": [
                  {
                    "text": "Klaim Asuransi Kesehatan",
                    "additionalFields": {
                      "callback_data": "asuransi"
                    }
                  }
                ]
              }
            },
            {
              "row": {
                "buttons": [
                  {
                    "text": "Permintaan Alat Kerja Baru",
                    "additionalFields": {
                      "callback_data": "alat_kerja"
                    }
                  }
                ]
              }
            }
          ]
        },
        "additionalFields": {}
      },
      "type": "n8n-nodes-base.telegram",
      "typeVersion": 1.2,
      "position": [
        -656,
        240
      ],
      "id": "c7cab36a-ac87-4c8b-b18e-5049b1368f31",
      "name": "true",
      "webhookId": "09aecdab-839b-494e-aa2f-07b89ef87f76",
      "credentials": {
        "telegramApi": {
          "id": "n7cxOzcieENzevJa",
          "name": "mark lee"
        }
      }
    },
    {
      "parameters": {
        "chatId": "1535237765",
        "text": "Untuk memulai percakapan, harap ketik /start",
        "additionalFields": {}
      },
      "type": "n8n-nodes-base.telegram",
      "typeVersion": 1.2,
      "position": [
        -656,
        368
      ],
      "id": "eda42da7-0a16-4ef2-945c-c7a3c5dcaef1",
      "name": "false",
      "webhookId": "09aecdab-839b-494e-aa2f-07b89ef87f76",
      "credentials": {
        "telegramApi": {
          "id": "n7cxOzcieENzevJa",
          "name": "mark lee"
        }
      }
    },
    {
      "parameters": {
        "assignments": {
          "assignments": [
            {
              "id": "27c861f3-8b5e-4455-865e-f1abc93d0575",
              "name": "reimbursement",
              "value": "=Karyawan harus mengisi formulir, melampirkan bukti bayar asli, dan menyerahkannya ke manajer. Pembayaran akan di proses dalam 14 hari kerja.",
              "type": "string"
            }
          ]
        },
        "options": {}
      },
      "type": "n8n-nodes-base.set",
      "typeVersion": 3.4,
      "position": [
        -1120,
        528
      ],
      "id": "d09dba78-1482-4547-b61c-61a88ef02950",
      "name": "Reimbursement"
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
              "id": "5a9aa60e-82ee-4d4d-9073-f35d4168d113",
              "leftValue": "={{ $json.reimbursement }}",
              "rightValue": "=reimbursement",
              "operator": {
                "type": "string",
                "operation": "equals"
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
        -912,
        528
      ],
      "id": "f9ce24bf-ffd7-41d7-9bc1-e96bc1787a22",
      "name": "true reimbursement"
    },
    {
      "parameters": {
        "chatId": "{{ $json.callback_query.data }}",
        "text": "={{ $json.reimbursement }}",
        "additionalFields": {}
      },
      "type": "n8n-nodes-base.telegram",
      "typeVersion": 1.2,
      "position": [
        -656,
        512
      ],
      "id": "82a04700-104c-4f7f-818c-f8b62e1d09b3",
      "name": "Send a text message",
      "webhookId": "65e91edd-096b-413e-874a-675f7b1dbd08",
      "credentials": {
        "telegramApi": {
          "id": "n7cxOzcieENzevJa",
          "name": "mark lee"
        }
      }
    },
    {
      "parameters": {
        "assignments": {
          "assignments": [
            {
              "id": "8e69594d-2017-4371-a885-40e1549b6b50",
              "name": "cuti",
              "value": "Karyawan harus mengajukan cuti melalui portal HRD",
              "type": "string"
            }
          ]
        },
        "options": {}
      },
      "type": "n8n-nodes-base.set",
      "typeVersion": 3.4,
      "position": [
        -1344,
        784
      ],
      "id": "38845afa-8b18-4d89-bf33-4074214d03bb",
      "name": "Cuti"
    },
    {
      "parameters": {
        "chatId": "{{ $('Telegram Trigger').item.json.message.chat.id }}",
        "text": "={{ $json.cuti }}",
        "additionalFields": {}
      },
      "type": "n8n-nodes-base.telegram",
      "typeVersion": 1.2,
      "position": [
        -656,
        768
      ],
      "id": "743ed17a-1119-4033-ac04-bac9f365176f",
      "name": "Send a text message1",
      "webhookId": "ba5c23bc-6146-4356-9e7d-3aed23490c1f",
      "credentials": {
        "telegramApi": {
          "id": "n7cxOzcieENzevJa",
          "name": "mark lee"
        }
      }
    },
    {
      "parameters": {
        "assignments": {
          "assignments": [
            {
              "id": "702dbfe0-eb4c-4c28-9e63-59e580dd3c34",
              "name": "lembur",
              "value": "Lembur harus mendapat persetujuan atasan terlebih dahulu",
              "type": "string"
            }
          ]
        },
        "options": {}
      },
      "type": "n8n-nodes-base.set",
      "typeVersion": 3.4,
      "position": [
        -896,
        928
      ],
      "id": "61a68b38-721a-4ae0-9a07-cd0ef579fe08",
      "name": "Lembur"
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
              "id": "7407525f-7b9b-41c4-8f13-f4625002ce24",
              "leftValue": "={{ $json.lembur }}",
              "rightValue": "lembur",
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
        -656,
        928
      ],
      "id": "c8b4be32-271d-4144-bdad-0dad55fc105f",
      "name": "true lembur"
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
              "id": "5a9aa60e-82ee-4d4d-9073-f35d4168d113",
              "leftValue": "={{ $json.cuti }}",
              "rightValue": "cuti",
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
        -1136,
        784
      ],
      "id": "9a446f14-430b-46f2-b416-d67cdd7f48be",
      "name": "true cuti"
    },
    {
      "parameters": {
        "chatId": "{{ $('Telegram Trigger').item.json.message.chat.id }}",
        "text": "={{ $json.lembur }}",
        "additionalFields": {}
      },
      "type": "n8n-nodes-base.telegram",
      "typeVersion": 1.2,
      "position": [
        -432,
        912
      ],
      "id": "cdf47753-eb56-4664-8fbb-22c04ab6fcb5",
      "name": "Send a text message2",
      "webhookId": "ba5c23bc-6146-4356-9e7d-3aed23490c1f",
      "credentials": {
        "telegramApi": {
          "id": "n7cxOzcieENzevJa",
          "name": "mark lee"
        }
      }
    },
    {
      "parameters": {
        "assignments": {
          "assignments": [
            {
              "id": "11c623bf-e886-4116-b05a-5ff73b7ade96",
              "name": "asuransi",
              "value": "Karyawan wajib membawa kartu asuransi, mengisi fo",
              "type": "string"
            }
          ]
        },
        "options": {}
      },
      "type": "n8n-nodes-base.set",
      "typeVersion": 3.4,
      "position": [
        -1360,
        1168
      ],
      "id": "b8766d1a-3006-4ec4-8906-844612ef54d5",
      "name": "Asuransi"
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
              "id": "7407525f-7b9b-41c4-8f13-f4625002ce24",
              "leftValue": "={{ $json.asuransi }}",
              "rightValue": "asuransi",
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
        -1168,
        1168
      ],
      "id": "3e93e610-11e4-432a-8326-68afc0370c69",
      "name": "true asuransi"
    },
    {
      "parameters": {
        "chatId": "{{ $('Telegram Trigger').item.json.message.chat.id }}",
        "text": "={{ $json.asuransi }}",
        "additionalFields": {}
      },
      "type": "n8n-nodes-base.telegram",
      "typeVersion": 1.2,
      "position": [
        -928,
        1152
      ],
      "id": "b00420b8-5153-4aba-9883-0a4c9b124d4e",
      "name": "Send a text message3",
      "webhookId": "ba5c23bc-6146-4356-9e7d-3aed23490c1f",
      "credentials": {
        "telegramApi": {
          "id": "n7cxOzcieENzevJa",
          "name": "mark lee"
        }
      }
    },
    {
      "parameters": {
        "assignments": {
          "assignments": [
            {
              "id": "c76ad5ea-a6d5-4421-9341-00716bedbb3f",
              "name": "alat_kerja",
              "value": "Karyawan mengajukan permintaan melalui sistem yang ada",
              "type": "string"
            }
          ]
        },
        "options": {}
      },
      "type": "n8n-nodes-base.set",
      "typeVersion": 3.4,
      "position": [
        -928,
        1344
      ],
      "id": "02f61845-570e-4577-a3bf-8ff3d2347fc6",
      "name": "Alat Kerja"
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
              "id": "7407525f-7b9b-41c4-8f13-f4625002ce24",
              "leftValue": "={{ $json.alat_kerja }}",
              "rightValue": "alat_kerja",
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
        -736,
        1344
      ],
      "id": "bd06daa5-2710-42d5-a18f-38ce006e3c07",
      "name": "true alat_kerja"
    },
    {
      "parameters": {
        "chatId": "1535237765",
        "text": "={{ $json.alat_kerja }}",
        "additionalFields": {}
      },
      "type": "n8n-nodes-base.telegram",
      "typeVersion": 1.2,
      "position": [
        -512,
        1328
      ],
      "id": "5d517707-d9ba-40bf-8cfc-042d92ecc3de",
      "name": "Send a text message4",
      "webhookId": "ba5c23bc-6146-4356-9e7d-3aed23490c1f",
      "credentials": {
        "telegramApi": {
          "id": "n7cxOzcieENzevJa",
          "name": "mark lee"
        }
      }
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
            "node": "Reimbursement",
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
            "node": "true",
            "type": "main",
            "index": 0
          }
        ],
        [
          {
            "node": "false",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Reimbursement": {
      "main": [
        [
          {
            "node": "true reimbursement",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "true reimbursement": {
      "main": [
        [
          {
            "node": "Send a text message",
            "type": "main",
            "index": 0
          }
        ],
        [
          {
            "node": "Cuti",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Cuti": {
      "main": [
        [
          {
            "node": "true cuti",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Lembur": {
      "main": [
        [
          {
            "node": "true lembur",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "true lembur": {
      "main": [
        [
          {
            "node": "Send a text message2",
            "type": "main",
            "index": 0
          }
        ],
        [
          {
            "node": "Asuransi",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "true cuti": {
      "main": [
        [
          {
            "node": "Send a text message1",
            "type": "main",
            "index": 0
          }
        ],
        [
          {
            "node": "Lembur",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Asuransi": {
      "main": [
        [
          {
            "node": "true asuransi",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "true asuransi": {
      "main": [
        [
          {
            "node": "Send a text message3",
            "type": "main",
            "index": 0
          }
        ],
        [
          {
            "node": "Alat Kerja",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Send a text message3": {
      "main": [
        []
      ]
    },
    "Alat Kerja": {
      "main": [
        [
          {
            "node": "true alat_kerja",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "true alat_kerja": {
      "main": [
        [
          {
            "node": "Send a text message4",
            "type": "main",
            "index": 0
          }
        ]
      ]
    }
  },
  "pinData": {},
  "meta": {
    "instanceId": "f9c216ef2c5ce3632c1ddcbc770aee702ab0e63a38eea8ec506f2d08fc35dd05"
  }
}
