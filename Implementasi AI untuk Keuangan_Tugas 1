{
  "nodes": [
    {
      "parameters": {
        "formTitle": "Pembuatan Invoice Otomatis",
        "formFields": {
          "values": [
            {
              "fieldLabel": "Nama Klien"
            },
            {
              "fieldLabel": "Jam Kerja",
              "requiredField": true
            },
            {
              "fieldLabel": "Rate"
            },
            {
              "fieldLabel": "Email Klien"
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
      "id": "11950740-ecd3-4b25-906f-eefbc68c3d4b",
      "name": "On form submission",
      "webhookId": "cc7b86d7-044d-4911-82bc-653362a26f58"
    },
    {
      "parameters": {
        "options": {}
      },
      "type": "n8n-nodes-base.set",
      "typeVersion": 3.4,
      "position": [
        208,
        0
      ],
      "id": "c0eca9ea-ce01-4416-ba2f-640bdac6b22c",
      "name": "Edit Fields"
    },
    {
      "parameters": {
        "html": "<!DOCTYPE html>\n<html>\n<html lang=\"id\">\n<head>\n  <meta charset=\"UTF-8\">\n  <title>Invoice</title>\n  <style>\n    body {\n      font-family: Arial, Helvetica, sans-serif;\n      background: #f4f6f8;\n      padding: 40px;\n      color: #333;\n    }\n\n    .invoice-wrapper {\n      max-width: 800px;\n      margin: auto;\n      background: #ffffff;\n      border-radius: 8px;\n      padding: 40px;\n      box-shadow: 0 4px 12px rgba(0,0,0,0.08);\n    }\n\n    .invoice-header {\n      display: flex;\n      justify-content: space-between;\n      align-items: center;\n      border-bottom: 2px solid #eaeaea;\n      padding-bottom: 20px;\n      margin-bottom: 30px;\n    }\n\n    .invoice-header h1 {\n      margin: 0;\n      font-size: 28px;\n      color: #1f2937;\n      letter-spacing: 1px;\n    }\n\n    .invoice-meta {\n      text-align: right;\n      font-size: 14px;\n      color: #555;\n    }\n\n    .section {\n      margin-bottom: 30px;\n    }\n\n    .section-title {\n      font-size: 14px;\n      font-weight: bold;\n      color: #6b7280;\n      text-transform: uppercase;\n      margin-bottom: 8px;\n    }\n\n    .client-info p {\n      margin: 4px 0;\n      font-size: 15px;\n    }\n\n    table {\n      width: 100%;\n      border-collapse: collapse;\n      margin-top: 15px;\n    }\n\n    table thead th {\n      background: #f9fafb;\n      border-bottom: 2px solid #e5e7eb;\n      padding: 12px;\n      text-align: left;\n      font-size: 14px;\n    }\n\n    table tbody td {\n      padding: 12px;\n      border-bottom: 1px solid #e5e7eb;\n      font-size: 14px;\n    }\n\n    table th:nth-child(2),\n    table th:nth-child(3),\n    table th:nth-child(4),\n    table td:nth-child(2),\n    table td:nth-child(3),\n    table td:nth-child(4) {\n      text-align: right;\n    }\n\n    .total-box {\n      margin-top: 30px;\n      display: flex;\n      justify-content: flex-end;\n    }\n\n    .total-box table {\n      width: 300px;\n    }\n\n    .total-box td {\n      padding: 10px;\n      font-size: 15px;\n    }\n\n    .total-box tr:last-child td {\n      font-weight: bold;\n      font-size: 18px;\n      border-top: 2px solid #111827;\n    }\n\n    .footer {\n      margin-top: 50px;\n      font-size: 13px;\n      color: #6b7280;\n      text-align: center;\n    }\n  </style>\n</head>\n\n<body>\n  <div class=\"invoice-wrapper\">\n\n    <!-- HEADER -->\n    <div class=\"invoice-header\">\n      <h1>INVOICE</h1>\n      <div class=\"invoice-meta\">\n        <div>Tanggal: {{ $now }}</div>\n        <div>Invoice #: INV-{{ $execution.id }}</div>\n      </div>\n    </div>\n\n    <!-- CLIENT INFO -->\n    <div class=\"section client-info\">\n      <div class=\"section-title\">Ditagihkan Kepada</div>\n      <p><strong>{{ $('On form submission').item.json['Nama Klien'] }}</strong></p>\n      <p>{{ $('On form submission').item.json['Email Klien'] }}</p>\n    </div>\n\n    <!-- DETAIL TABLE -->\n    <div class=\"section\">\n      <div class=\"section-title\">Detail Pekerjaan</div>\n\n      <table>\n        <thead>\n          <tr>\n            <th>Deskripsi</th>\n            <th>Jam</th>\n            <th>Rate</th>\n            <th>Subtotal</th>\n          </tr>\n        </thead>\n        <tbody>\n          <tr>\n            <td>Jasa Pekerjaan / Konsultasi</td>\n            <td>{{ $('On form submission').item.json['Jam Kerja'] }}</td>\n            <td>{{ $('On form submission').item.json['Rate'] }}</td>\n            <td>{{ $json['Total Biaya'] }}</td>\n          </tr>\n        </tbody>\n      </table>\n    </div>\n\n    <!-- TOTAL -->\n    <div class=\"total-box\">\n      <table>\n        <tr>\n          <td>Total Tagihan</td>\n          <td style=\"text-align:right;\">\n            Rp {{ $json['Total Biaya'] }}\n          </td>\n        </tr>\n      </table>\n    </div>\n\n    <!-- FOOTER -->\n    <div class=\"footer\">\n      Invoice ini dibuat secara otomatis.<br>\n      Terima kasih atas kepercayaan Anda.\n    </div>\n\n  </div>\n</body>\n</html>\n"
      },
      "type": "n8n-nodes-base.html",
      "typeVersion": 1.2,
      "position": [
        416,
        0
      ],
      "id": "25c602a9-2ccb-448f-9129-a39522586320",
      "name": "HTML"
    },
    {
      "parameters": {
        "html_content": "={{ $json.html }}"
      },
      "type": "n8n-nodes-htmlcsstopdf.htmlcsstopdf",
      "typeVersion": 1,
      "position": [
        624,
        0
      ],
      "id": "59d6d9ac-3024-4b81-a8ec-8e0962ff1fde",
      "name": "Convert HTML to PDF",
      "credentials": {
        "htmlcsstopdfApi": {
          "id": "c7jQPbsfUEXToY6t",
          "name": "HTML to PDF account"
        }
      }
    },
    {
      "parameters": {
        "url": "={{ $json.pdf_url }}",
        "options": {}
      },
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 4.4,
      "position": [
        832,
        0
      ],
      "id": "597d69de-0c02-4a57-b459-ec4fd3c974df",
      "name": "HTTP Request"
    },
    {
      "parameters": {
        "sendTo": "={{ $('On form submission').item.json['Email Klien'] }}",
        "subject": "=Invoice dari Vedara Company untuk {{ $('On form submission').item.json['Nama Klien'] }}",
        "message": "=<p>Yth. <strong>{{ $('On form submission').item.json['Nama Klien'] }}</strong>,</p>  <p>Terima kasih atas kepercayaan Anda telah menggunakan jasa kami. <br> Bersama email ini, kami lampirkan invoice untuk pekerjaan yang telah diselesaikan.</p>  <p>Berikut adalah ringkasan singkat tagihan Anda:</p> <ul>     <li><strong>Total Jam Kerja:</strong>  {{ $('On form submission').item.json['Jam Kerja'] }}jam</li>     <li><strong>Total Tagihan:</strong> {{ $('Edit Fields').item.json['Total Biaya'] }}</li>     <li><strong>Jatuh Tempo:</strong> 14 hari</li> </ul>  <p>Detail lengkap, termasuk rincian pekerjaan dan instruksi pembayaran, dapat Anda temukan pada file PDF yang terlampir:{{ $json.pdf_url }}</p>  <blockquote style=\"border-left: 4px solid #ccc; padding-left: 15px; margin-left: 0; font-style: italic;\">   <strong>Catatan Keamanan:</strong> Untuk melindungi Anda, kami tidak akan pernah meminta informasi password atau data sensitif melalui email. Harap lakukan pembayaran hanya ke nomor rekening resmi yang tertera di dalam invoice PDF. </blockquote>  <p>Jika ada pertanyaan lebih lanjut, jangan ragu untuk membalas email ini.</p>  <p>Hormat kami,</p>  <p><strong>[Zen / Vedara Company]</strong><br> [Vedara / 123456789]</p>",
        "options": {
          "attachmentsUi": {
            "attachmentsBinary": [
              {}
            ]
          }
        }
      },
      "type": "n8n-nodes-base.gmail",
      "typeVersion": 2.2,
      "position": [
        1040,
        0
      ],
      "id": "b884c723-01b6-4deb-b27f-87b91bea1b48",
      "name": "Send a message",
      "webhookId": "e4e19caa-0538-409a-9771-4be52fb2df75",
      "credentials": {
        "gmailOAuth2": {
          "id": "hmMIdCyXQA9NBJ1J",
          "name": "Gmail account"
        }
      }
    }
  ],
  "connections": {
    "On form submission": {
      "main": [
        [
          {
            "node": "Edit Fields",
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
            "node": "HTML",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "HTML": {
      "main": [
        [
          {
            "node": "Convert HTML to PDF",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Convert HTML to PDF": {
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
            "node": "Send a message",
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
