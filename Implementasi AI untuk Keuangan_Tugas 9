{
  "nodes": [
    {
      "parameters": {
        "rule": {
          "interval": [
            {
              "triggerAtHour": 9
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
      "id": "b2276a1d-d67d-4064-a3d2-1e31af2f841f",
      "name": "Schedule Trigger"
    },
    {
      "parameters": {
        "mode": "raw",
        "jsonOutput": "{\n  \"symbols\": [\"AAPL\",\n  \"TSLA\", MSFT]\n}\n",
        "options": {}
      },
      "type": "n8n-nodes-base.set",
      "typeVersion": 3.4,
      "position": [
        208,
        0
      ],
      "id": "82fc58f6-6cb3-48dd-b8b9-1b56a676c740",
      "name": "Watchlist"
    },
    {
      "parameters": {
        "url": "={{`https://query1.finance.yahoo.com/v8/finance/chart/${$json.symbols[0]}`}}",
        "sendQuery": true,
        "queryParameters": {
          "parameters": [
            {
              "name": "range",
              "value": "6mo"
            },
            {
              "name": "interval",
              "value": "1d"
            }
          ]
        },
        "sendHeaders": true,
        "headerParameters": {
          "parameters": [
            {
              "name": "User-Agent",
              "value": "Mozilla/5.0"
            },
            {
              "name": "Accept",
              "value": "application/json"
            }
          ]
        },
        "options": {}
      },
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 4.4,
      "position": [
        416,
        -144
      ],
      "id": "adae85d1-a8f3-4e59-b78a-97a04b9901bd",
      "name": "AAPL"
    },
    {
      "parameters": {
        "url": "={{`https://query1.finance.yahoo.com/v8/finance/chart/${$json.symbols[2]}`}}",
        "sendQuery": true,
        "queryParameters": {
          "parameters": [
            {
              "name": "range",
              "value": "6mo"
            },
            {
              "name": "interval",
              "value": "1d"
            }
          ]
        },
        "sendHeaders": true,
        "headerParameters": {
          "parameters": [
            {
              "name": "User-Agent",
              "value": "Mozilla/5.0"
            },
            {
              "name": "Accept",
              "value": "application/json"
            }
          ]
        },
        "options": {}
      },
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 4.4,
      "position": [
        416,
        144
      ],
      "id": "5983c0e6-9833-4f8a-8ef1-ab5074d723c4",
      "name": "AAPL2"
    },
    {
      "parameters": {
        "url": "={{`https://query1.finance.yahoo.com/v8/finance/chart/${$json.symbols[1]}`}}",
        "sendQuery": true,
        "queryParameters": {
          "parameters": [
            {
              "name": "range",
              "value": "6mo"
            },
            {
              "name": "interval",
              "value": "1d"
            }
          ]
        },
        "sendHeaders": true,
        "headerParameters": {
          "parameters": [
            {
              "name": "User-Agent",
              "value": "Mozilla/5.0"
            },
            {
              "name": "Accept",
              "value": "application/json"
            }
          ]
        },
        "options": {}
      },
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 4.4,
      "position": [
        416,
        0
      ],
      "id": "dbcc49a4-7afb-4111-86af-7c3391d6b9a8",
      "name": "TSLA"
    },
    {
      "parameters": {
        "numberInputs": 3
      },
      "type": "n8n-nodes-base.merge",
      "typeVersion": 3.2,
      "position": [
        608,
        -16
      ],
      "id": "75d34582-8287-4ed6-b026-cd3158a0aa7b",
      "name": "Merge"
    },
    {
      "parameters": {
        "jsCode": "// Ambil semua item hasil merge\nconst results = items.map(item => item.json);\n\n// Helper functions\nfunction SMA(data, period) {\n  return data.map((_, i, arr) => {\n    if (i < period) return null;\n    const slice = arr.slice(i - period, i);\n    return slice.reduce((a, b) => a + b, 0) / period;\n  });\n}\n\nfunction RSI(data, period = 14) {\n  const gains = [], losses = [];\n  for (let i = 1; i < data.length; i++) {\n    const diff = data[i] - data[i - 1];\n    gains.push(diff > 0 ? diff : 0);\n    losses.push(diff < 0 ? -diff : 0);\n  }\n  if (gains.length < period) return null;\n  let avgGain = gains.slice(0, period).reduce((a,b)=>a+b,0)/period;\n  let avgLoss = losses.slice(0, period).reduce((a,b)=>a+b,0)/period;\n  for (let i = period; i < gains.length; i++) {\n    avgGain = (avgGain * (period - 1) + gains[i]) / period;\n    avgLoss = (avgLoss * (period - 1) + losses[i]) / period;\n  }\n  const rs = avgGain / (avgLoss || 1);\n  return 100 - 100 / (1 + rs);\n}\n\nconst output = [];\n\nfor (const data of results) {\n  try {\n    // result adalah chart.result[0] jika ada\n    const result = data.chart?.result?.[0];\n\n    // > SKIP jika tidak ada chart/result\n    if (!result) {\n      output.push({ json: { error: 'No chart/result for one item', raw: data } });\n      continue;\n    }\n\n    // Symbol seharusnya ada di result.meta.symbol (Yahoo)\n    const symbol = result.meta?.symbol || data.symbol || data.meta?.symbol || 'UNKNOWN';\n\n    // Dapatkan closes, safety checks\n    const closesRaw = result.indicators?.quote?.[0]?.close;\n    if (!closesRaw || !Array.isArray(closesRaw)) {\n      output.push({ json: { symbol, error: 'No close prices in response' } });\n      continue;\n    }\n    const closes = closesRaw.filter(v => v !== null && v !== undefined);\n\n    // Pastikan cukup data untuk MA200; kalau tidak, beri flag\n    if (closes.length < 50) {\n      output.push({ json: { symbol, error: 'Not enough candles', candles: closes.length } });\n      continue;\n    }\n\n    // Hitung indikator\n    const ma50 = SMA(closes, 50);\n    const ma200 = SMA(closes, 200);\n    const lastClose = closes.at(-1);\n    const lastMA50 = ma50.filter(v => v !== null).at(-1) || null;\n    const lastMA200 = ma200.filter(v => v !== null).at(-1) || null;\n    const rsi = RSI(closes, 14);\n\n    // Tentukan sinyal (prioritas RSI dulu)\n    let signal = '⚪ Tidak ada sinyal saat ini';\n    if (rsi !== null && rsi < 30) signal = '🔵 RSI Oversold (Potensi Buy)';\n    else if (rsi !== null && rsi > 70) signal = '🔴 RSI Overbought (Potensi Sell)';\n    else if (lastMA50 !== null && lastMA200 !== null && lastMA50 > lastMA200) signal = '🟢 Golden Cross (Buy Signal)';\n    else if (lastMA50 !== null && lastMA200 !== null && lastMA50 < lastMA200) signal = '🔻 Death Cross (Sell Signal)';\n\n    output.push({\n      json: {\n        symbol,\n        lastClose,\n        rsi: rsi !== null ? Number(rsi.toFixed(2)) : null,\n        ma50: lastMA50 !== null ? Number(lastMA50.toFixed(2)) : null,\n        ma200: lastMA200 !== null ? Number(lastMA200.toFixed(2)) : null,\n        signal\n      }\n    });\n  } catch (err) {\n    output.push({ json: { error: err.message } });\n  }\n}\n\nreturn output;\n"
      },
      "type": "n8n-nodes-base.code",
      "typeVersion": 2,
      "position": [
        800,
        0
      ],
      "id": "cbcd7c26-afd7-457f-8cb4-07f7d4dbfee9",
      "name": "Analyze Signals Stocks"
    },
    {
      "parameters": {
        "chatId": "1535237765",
        "text": "=📊 Symbol: {{$json[\"symbol\"]}}  💰 Harga terakhir: {{$json[\"lastClose\"]}} 📈 RSI: {{$json[\"rsi\"]}} 📊 MA50: {{$json[\"ma50\"]}} 📊 MA200: {{$json[\"ma200\"]}}  🚨 Sinyal: {{$json[\"signal\"]}}",
        "additionalFields": {}
      },
      "type": "n8n-nodes-base.telegram",
      "typeVersion": 1.2,
      "position": [
        1008,
        0
      ],
      "id": "3445c0be-283d-41b3-90c7-6ee306ef244e",
      "name": "Telegram (Stocks)",
      "webhookId": "094221f0-21f6-465c-8763-5e3b9cf04364",
      "credentials": {
        "telegramApi": {
          "id": "n7cxOzcieENzevJa",
          "name": "mark lee"
        }
      }
    },
    {
      "parameters": {
        "rule": {
          "interval": [
            {
              "triggerAtHour": 9
            }
          ]
        }
      },
      "type": "n8n-nodes-base.scheduleTrigger",
      "typeVersion": 1.3,
      "position": [
        288,
        320
      ],
      "id": "585d550b-8e3d-41e0-8217-7a0e9dd09f9c",
      "name": "Schedule Trigger1"
    },
    {
      "parameters": {
        "jsCode": "// === Ambil data harga dari Yahoo Finance ===\nconst data = items[0].json.chart?.result?.[0];\nif (!data) {\n  return [{ json: { error: \"❌ Tidak ada data dari Yahoo Finance.\" } }];\n}\n\nconst closes = data.indicators.quote[0].close.filter(v => v !== null);\n\n// === Fungsi bantu ===\nfunction SMA(data, period) {\n  return data.map((_, i, arr) => {\n    if (i < period) return null;\n    const slice = arr.slice(i - period, i);\n    return slice.reduce((a, b) => a + b, 0) / period;\n  });\n}\n\nfunction RSI(data, period = 14) {\n  let gains = [], losses = [];\n  for (let i = 1; i < data.length; i++) {\n    const diff = data[i] - data[i - 1];\n    gains.push(diff > 0 ? diff : 0);\n    losses.push(diff < 0 ? -diff : 0);\n  }\n\n  if (gains.length < period) return null;\n\n  let avgGain = gains.slice(0, period).reduce((a, b) => a + b, 0) / period;\n  let avgLoss = losses.slice(0, period).reduce((a, b) => a + b, 0) / period;\n\n  for (let i = period; i < gains.length; i++) {\n    avgGain = (avgGain * (period - 1) + gains[i]) / period;\n    avgLoss = (avgLoss * (period - 1) + losses[i]) / period;\n  }\n\n  const rs = avgGain / (avgLoss || 1);\n  return 100 - 100 / (1 + rs);\n}\n\n// === Hitung indikator ===\nconst ma50 = SMA(closes, 50);\nconst ma200 = SMA(closes, 200);\n\nconst lastClose = closes.at(-1);\nconst lastMA50 = ma50.at(-1);\nconst lastMA200 = ma200.filter(v => v !== null).at(-1) || lastMA50;\nconst rsi = RSI(closes, 14);\n\n// === Tentukan sinyal ===\nlet signal = \"⚪ Tidak ada sinyal saat ini\";\nif (rsi && rsi < 30) signal = \"🔵 RSI Oversold (Potensi Buy)\";\nelse if (rsi && rsi > 70) signal = \"🔴 RSI Overbought (Potensi Sell)\";\nelse if (lastMA50 > lastMA200) signal = \"🟢 Golden Cross (Buy Signal)\";\nelse if (lastMA50 < lastMA200) signal = \"🔻 Death Cross (Sell Signal)\";\n\n// === Return hasil ===\nreturn [{\n  json: {\n    symbol: data.meta.symbol || \"BTC-USD\",\n    lastClose,\n    rsi: rsi ? rsi.toFixed(2) : null,\n    ma50: lastMA50 ? lastMA50.toFixed(2) : null,\n    ma200: lastMA200 ? lastMA200.toFixed(2) : null,\n    signal\n  }\n}];\n\n"
      },
      "type": "n8n-nodes-base.code",
      "typeVersion": 2,
      "position": [
        640,
        320
      ],
      "id": "26eb6382-93a0-416f-b01a-39f4615bf36e",
      "name": "Analyze Signals BTC"
    },
    {
      "parameters": {
        "chatId": "1535237765",
        "text": "=📊 [BTC-USD] Sinyal 5m  💰 Harga terakhir: {{$json[\"lastClose\"]}} 📈 RSI: {{$json[\"rsi\"]}} 📊 MA50: {{$json[\"ma50\"]}} 📊 MA200: {{$json[\"ma200\"]}}  🚨 Sinyal: {{$json[\"signal\"]}}",
        "additionalFields": {}
      },
      "type": "n8n-nodes-base.telegram",
      "typeVersion": 1.2,
      "position": [
        848,
        320
      ],
      "id": "edbc38c0-5227-475c-8372-6984763abdce",
      "name": "BTC",
      "webhookId": "c8b2efc2-9076-4ead-9bd2-b6c53c589caa",
      "credentials": {
        "telegramApi": {
          "id": "n7cxOzcieENzevJa",
          "name": "mark lee"
        }
      }
    },
    {
      "parameters": {
        "url": "=https://query1.finance.yahoo.com/v8/finance/chart/BTC-USD",
        "sendQuery": true,
        "queryParameters": {
          "parameters": [
            {
              "name": "range",
              "value": "6mo"
            },
            {
              "name": "interval",
              "value": "1d"
            }
          ]
        },
        "sendHeaders": true,
        "headerParameters": {
          "parameters": [
            {
              "name": "User-Agent",
              "value": "Mozilla/5.0"
            },
            {
              "name": "Accept",
              "value": "application/json"
            }
          ]
        },
        "options": {}
      },
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 4.4,
      "position": [
        464,
        320
      ],
      "id": "420b9a65-21ed-470c-ba8d-b68a61ba4429",
      "name": "BTC/USD"
    }
  ],
  "connections": {
    "Schedule Trigger": {
      "main": [
        [
          {
            "node": "Watchlist",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Watchlist": {
      "main": [
        [
          {
            "node": "AAPL",
            "type": "main",
            "index": 0
          },
          {
            "node": "TSLA",
            "type": "main",
            "index": 0
          },
          {
            "node": "AAPL2",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "AAPL": {
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
    "AAPL2": {
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
    "TSLA": {
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
    "Merge": {
      "main": [
        [
          {
            "node": "Analyze Signals Stocks",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Analyze Signals Stocks": {
      "main": [
        [
          {
            "node": "Telegram (Stocks)",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Schedule Trigger1": {
      "main": [
        [
          {
            "node": "BTC/USD",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Analyze Signals BTC": {
      "main": [
        [
          {
            "node": "BTC",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "BTC/USD": {
      "main": [
        [
          {
            "node": "Analyze Signals BTC",
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
