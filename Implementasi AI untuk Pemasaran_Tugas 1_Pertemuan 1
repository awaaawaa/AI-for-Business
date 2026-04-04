{
  "nodes": [
    {
      "parameters": {
        "formTitle": "Pendaftaran SIB Mandiri Batch 6",
        "formFields": {
          "values": [
            {
              "fieldLabel": "Nama",
              "fieldName": "Nama",
              "placeholder": "=",
              "requiredField": true
            },
            {
              "fieldLabel": "Email",
              "fieldName": "Email",
              "requiredField": true
            },
            {
              "fieldLabel": "Kelas",
              "fieldType": "dropdown",
              "fieldName": "Kelas",
              "fieldOptions": {
                "values": [
                  {
                    "option": "AI for Business"
                  },
                  {
                    "option": "Codeless Data Science"
                  },
                  {
                    "option": "DevOps Engineer"
                  },
                  {
                    "option": "Digital Marketing"
                  },
                  {
                    "option": "Fullstack Web Developer"
                  },
                  {
                    "option": "Mobile App Developer"
                  }
                ]
              },
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
      "id": "ba614650-2eac-4f96-9e10-6f16efca1b98",
      "name": "On form submission",
      "webhookId": "c46a7417-a199-471e-97d5-2981d2685a30"
    },
    {
      "parameters": {
        "sendTo": "='{{ $json.Email }}",
        "subject": "Informasi Pendaftaran SIB NF Academy Batch 6",
        "message": "=<!DOCTYPE html> <html> <head>   <style>     /* Reset dasar untuk kompatibilitas email client */     body { margin: 0; padding: 0; font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; background-color: #f0ebf8; }     .container { max-width: 600px; margin: 0 auto; background-color: #ffffff; border-radius: 8px; overflow: hidden; box-shadow: 0 2px 5px rgba(0,0,0,0.1); }     .header { background-color: #673ab7; /* Warna Ungu Google Form */ color: #ffffff; padding: 24px; text-align: center; }     .header h1 { margin: 0; font-size: 20px; font-weight: 600; }     .content { padding: 30px; color: #333333; line-height: 1.6; }     .data-box { background-color: #f8f9fa; border-left: 4px solid #673ab7; padding: 15px; margin: 20px 0; border-radius: 4px; }     .data-row { margin-bottom: 10px; }     .label { font-weight: bold; color: #5f6368; font-size: 14px; }     .value { color: #202124; font-size: 16px; }     .footer { background-color: #f8f9fa; padding: 20px; text-align: center; font-size: 12px; color: #888888; border-top: 1px solid #eeeeee; }     .button { display: inline-block; background-color: #673ab7; color: #ffffff; text-decoration: none; padding: 10px 20px; border-radius: 4px; margin-top: 20px; font-weight: bold; }   </style> </head> <body>    <div class=\"container\">     <div class=\"header\">       <h1>Konfirmasi Pendaftaran<br>SIB Mandiri Batch 4 NF Academy</h1>     </div>      <div class=\"content\">       <p>Halo <strong>{{ $json[\"Nama\"] }}</strong>,</p>              <p>Terima kasih telah melakukan pendaftaran. Data Anda telah berhasil kami terima di sistem NF Academy.</p>              <p>Berikut adalah rincian data yang Anda kirimkan:</p>        <div class=\"data-box\">         <div class=\"data-row\">           <div class=\"label\">Nama Lengkap</div>           <div class=\"value\">{{ $json[\"Nama\"] }}</div>         </div>                  <div class=\"data-row\">           <div class=\"label\">Email Terdaftar</div>           <div class=\"value\">{{ $json[\"Email\"] }}</div>         </div>          <div class=\"data-row\">           <div class=\"label\">Kelas Pilihan</div>           <div class=\"value\">{{ $json[\"Kelas\"] }}</div>         </div>       </div>        <p>Mohon cek kembali data di atas. Jika ada kesalahan atau pertanyaan lebih lanjut, silakan balas email ini.</p>              <p>Selanjutnya, tim kami akan melakukan verifikasi dan menghubungi Anda untuk langkah berikutnya.</p>              <br>       <p>Salam hangat,<br><strong>Tim Penerimaan NF Academy</strong></p>     </div>      <div class=\"footer\">       &copy; 2025 NF Academy. All rights reserved.<br>       Email ini dikirim secara otomatis melalui sistem pendaftaran.     </div>   </div>  </body> </html>",
        "options": {}
      },
      "type": "n8n-nodes-base.gmail",
      "typeVersion": 2.2,
      "position": [
        208,
        0
      ],
      "id": "36d14bd5-e8cc-49f9-9164-1a7f0865cb46",
      "name": "Send a message",
      "webhookId": "9a86dad7-6c58-401a-a58f-25c931494f92",
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
