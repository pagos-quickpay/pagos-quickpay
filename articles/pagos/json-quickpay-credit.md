## Ejemplo petición payment_method": "QUICKPAY_CREDIT"

```
curl -X POST \
  https://api.qa.peinau.fif.tech/checkout/payments \
  -H 'authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJwcmltYXJ5c2lkIjoiMjhhZGI5OTktN2EyZS03MGI4LWMwOTItZTRjMTZhOWU5ZTBhIiwidW5pcXVlX25hbWUiOiJUb2lwYXRvLmNvbSIsImdyb3Vwc2lkIjoiQVBQTCIsImlzcyI6IkZhbGFiZWxsYSIsImF1ZCI6IldlYiIsInR5cGUiOiJCZWFyZXIiLCJzY29wZSI6W10sImlhdCI6MTUxMzE3Nzk1OCwiZXhwIjoxNTEzMTc4ODU4fQ.OYBksNEvNBU012fJt4IhUnQ5g0szPXPmivD2GvprLczjbG6Pd7HeSyWddSCVOAwAXfycNMzwn0nb_6VdYMqbSzE3T9Bu0Oqzih4b_BfLLb4EwpRQ3L0ObFNkJTI2hfIMUNJQ5ohT8b2yR-1SiehAUd0Tlkb3zrh2aDP9AYVZGqkjLdnwQOpBtXVs6VmntXnb3_MklOU7U0BylB1kVG40t9qfSxf79DYTcr3JWs6LdCFDThkudMZtJfnjYsOoqt--Iv8BzhCU7Eft1Isf2Qfqn_1-p778E7r4yQY1GREuAsXPNfnnHxi7gOVVQ1owq1aekqt4m4ML-VLow8pUx5duYw' \
  -H 'content-type: application/json' \
  -d '{
  "payer": {
    "payer_info": {
      "email": "aroa@gmail.com",
      "full_name": "Andres Roa",
      "country": "CL",
      "document_number": "346055871",
      "document_type": "RUT",
      "is_guest": "true"
    },
    "payment_method": "QUICKPAY_CREDIT"
  },
  "transaction": {
    "reference_id": null,
    "description": "Smartv",
    "soft_descriptor": "Sony Smartv",
    "amount": {
      "currency": "CLP",
      "total": 7200,
      "details": {
        "subtotal": 7200,
        "tax": 0,
        "shipping": 0,
        "shipping_discount": 0
      }
    },
    "item_list": {
      "shipping_address": {
        "line1": "Av. Las Condes 0225, Las Condes",
        "city": "Chile",
        "country_code": "CL",
        "phone": "+56955545899",
        "type": "HOME_OR_WORK",
        "recipient_name": "Andres Roa"
      },
      "shipping_method": "PICK_IN_PLACE",
      "items": [
        {
          "sku": "117110",
          "name": "TV Sony",
          "description": "TV Sony",
          "quantity": 1,
          "price": 7200,
          "tax": 0
        }
      ]
    },
    "gateway_order": "900000065434"
  },
  "redirect_urls": {
    "return_url": "https://web.segurosfalabella.com/co/",
    "cancel_url": "https://www.falabella.com.co/falabella-co/"
  },
  "intent": "sale",
  "additional_attributes": {
    "installments_offer": [
      "1",
      "3"
    ],
    "installments_without_interest": [
      "3"
    ],
    "default_installment_number": "1",
    "default_deferred_month": "3",
    "is_deferred_capture": "false"
  }
}'
 
```
 
A continuación se presenta ejemplo de un JSON de respuesta obtenido al crear una intención de pago a través de la API RESTful de checkout:

```
{
    "application": "5af0799cd1aa8e000f9de4ca",
    "_id": "5bd1ddeabae25c0015cb050c",
    "additional_attributes": {
        "is_deferred_capture": "false",
        "default_deferred_month": "3",
        "default_installment_number": "1",
        "installments_without_interest": [
            "3"
        ],
        "installments_offer": [
            "1",
            "3"
        ]
    },
    "redirect_urls": {
        "return_url": "https://web.segurosfalabella.com/co/",
        "cancel_url": "https://www.falabella.com.co/falabella-co/"
    },
    "transaction": {
        "reference_id": null,
        "description": "Smartv",
        "soft_descriptor": "Sony Smartv",
        "gateway_order": "900000065434",
        "item_list": {
            "shipping_method": "PICK_IN_PLACE",
            "items": [
                {
                    "sku": "117110",
                    "name": "TV Sony",
                    "description": "TV Sony",
                    "quantity": 1,
                    "price": 7200,
                    "tax": 0
                }
            ],
            "shipping_address": {
                "line1": "Av. Las Condes 0225, Las Condes",
                "city": "Chile",
                "country_code": "CL",
                "phone": "+56955545899",
                "type": "HOME_OR_WORK",
                "recipient_name": "Andres Roa"
            }
        },
        "amount": {
            "currency": "CLP",
            "total": 7200,
            "details": {
                "subtotal": 7200,
                "tax": 0,
                "shipping": 0,
                "shipping_discount": 0
            }
        }
    },
    "payer": {
        "payer_info": {
            "is_guest": "true",
            "document_type": "RUT",
            "document_number": "346055871",
            "country": "CL",
            "full_name": "Andres Roa",
            "email": "aroa@gmail.com"
        },
        "payment_method": "QUICKPAY_CREDIT"
    },
    "links": [
        {
            "href": "https://api.qa.peinau.fif.tech/checkout/payments/5bd1ddeabae25c0015cb050c",
            "rel": "self",
            "method": "GET"
        },
        {
            "href": "https://api.qa.peinau.fif.tech/checkout/payments/gateways/quickpay/credit_doc_id/5bd1ddeabae25c0015cb050c/pay",
            "rel": "approval_url",
            "method": "REDIRECT"
        },
        {
            "href": "https://api.qa.peinau.fif.tech/checkout/payments/5bd1ddeabae25c0015cb050c/edit",
            "rel": "update_url",
            "method": "PUT"
        },
        {
            "href": "https://api.qa.peinau.fif.tech/checkout/payments/gateways/quickpay/credit_doc_id/5bd1ddeabae25c0015cb050c/void",
            "rel": "void_method",
            "method": "POST"
        },
        {
            "href": "https://api.qa.peinau.fif.tech/checkout/payments/gateways/quickpay/credit_doc_id/5bd1ddeabae25c0015cb050c/refund",
            "rel": "refund_method",
            "method": "POST"
        },
        {
            "href": "https://api.qa.peinau.fif.tech/checkout/payments/900000065434",
            "rel": "self_by_gateway_order",
            "method": "GET"
        }
    ],
    "update_time": "2018-10-25T15:14:50.933Z",
    "create_time": "2018-10-25T15:14:50.933Z",
    "invoice_number": "IP-15404804909334111",
    "state": "created",
    "intent": "sale",
    "id": "5bd1ddeabae25c0015cb050c"
}
```
