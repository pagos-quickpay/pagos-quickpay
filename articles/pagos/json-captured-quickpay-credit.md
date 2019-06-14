## Ejemplo petición payment_method": "QUICKPAY_CREDIT" con captura previa

```
curl -X POST \
  https://api.qa.connect.fif.tech/checkout/payments \
  -H 'authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJwcmltYXJ5c2lkIjoiMjhhZGI5OTktN2EyZS03MGI4LWMwOTItZTRjMTZhOWU5ZTBhIiwidW5pcXVlX25hbWUiOiJUb2lwYXRvLmNvbSIsImdyb3Vwc2lkIjoiQVBQTCIsImlzcyI6IkZhbGFiZWxsYSIsImF1ZCI6IldlYiIsInR5cGUiOiJCZWFyZXIiLCJzY29wZSI6W10sImlhdCI6MTUxMzE3Nzk1OCwiZXhwIjoxNTEzMTc4ODU4fQ.OYBksNEvNBU012fJt4IhUnQ5g0szPXPmivD2GvprLczjbG6Pd7HeSyWddSCVOAwAXfycNMzwn0nb_6VdYMqbSzE3T9Bu0Oqzih4b_BfLLb4EwpRQ3L0ObFNkJTI2hfIMUNJQ5ohT8b2yR-1SiehAUd0Tlkb3zrh2aDP9AYVZGqkjLdnwQOpBtXVs6VmntXnb3_MklOU7U0BylB1kVG40t9qfSxf79DYTcr3JWs6LdCFDThkudMZtJfnjYsOoqt--Iv8BzhCU7Eft1Isf2Qfqn_1-p778E7r4yQY1GREuAsXPNfnnHxi7gOVVQ1owq1aekqt4m4ML-VLow8pUx5duYw' \
  -H 'content-type: application/json' \
  -d '{  
   "payer":{  
      "payer_info":{  
         "email":"dummy@gmail.com",
         "full_name":"Jhon Doe",
         "country":"CL",
         "document_number":"371119582",
         "document_type":"RUT",
         "is_guest": "true"
      },
      "payment_method":"QUICKPAY_CREDIT"
   },
   "transaction":{
      "reference_id":null,
      "description":"Transaction in app 789156083925170982900platform  QPAY id 0dfbb32c-2234-46e5-9e92-561511c00623",
      "soft_descriptor":"id 0dfbb32c-2234-46e5-9e92-561511c00623",
      "amount":{  
         "currency":"CLP",
         "total":1000,
         "details":{  
            "subtotal":1000,
            "tax":0,
            "shipping":0,
            "shipping_discount":0
         }
      },
      "item_list":{  
         "shipping_address":{  
            "line1":"Av. Las Condes 11049, Las Condes",
            "city":"Chile",
            "country_code":"CL",
            "phone":"+56956821215",
            "type":"HOME_OR_WORK",
            "recipient_name":"Jhon Doe"
         },
         "shipping_method":"PICK_IN_PLACE",
         "items":[  
            {  
               "sku":"117110",
               "name":"Cordu00f3n 3x1 mm 10 m metro lineal Negro",
               "description":"Cordu00f3n 3x1 mm 10 m metro lineal Negro",
               "quantity":1,
               "price":7200,
               "tax":0
            }
         ]
      }
   },
   "redirect_urls":{  
      "return_url":"https://www.falabella.com",
      "cancel_url":"https://www.google.com"
   },
   "intent":"sale",
   "purchase_order": {
    "purchase_order_id": "048375849305",
    "purchase_order_date": "2018-12-03T00:00:00-05:00"
   },   
   "additional_attributes":{  
      "capture_token": "b3718ffc-e542-416d-a02b-ddf9afb2a007",
      "installments_offer":[  
         "1",
         "2",
         "3",
         "4"
      ],
      "installments_without_interest":[  
         "2"
      ],
      "default_installment_number":"1",
      "default_deferred_month":"0",
      "is_deferred_capture":"false"
   }
}'
 
```
Importante a destacar el capture_token que fue recibido como parte de la captura hecha previamente.

 
A continuación se presenta ejemplo de un JSON de respuesta obtenido al crear una intención de pago a través de la API RESTful de checkout:

```
{
    "application": "5af350553dbed900146c5945",
    "_id": "5c0599e3ca2e140015a77689",
    "additional_attributes": {
        "is_deferred_capture": "true",
        "default_deferred_month": "0",
        "default_installment_number": "1",
        "installments_without_interest": [
            "2"
        ],
        "installments_offer": [
            "1",
            "2",
            "3",
            "4"
        ],
        "capture_token": "b3718ffc-e542-416d-a02b-ddf9afb2a007"
    },
    "redirect_urls": {
        "return_url": "https://www.falabella.com",
        "cancel_url": "https://www.google.com"
    },
    "transaction": {
        "gateway_order": "IP-15438709476584211",
        "reference_id": null,
        "description": "Transaction in app 789156083925170982900platform  QPAY id 0dfbb32c-2234-46e5-9e92-561511c00623",
        "soft_descriptor": "id 0dfbb32c-2234-46e5-9e92-561511c00623",
        "item_list": {
            "shipping_method": "PICK_IN_PLACE",
            "items": [
                {
                    "sku": "117110",
                    "name": "Cordu00f3n 3x1 mm 10 m metro lineal Negro",
                    "description": "Cordu00f3n 3x1 mm 10 m metro lineal Negro",
                    "quantity": 1,
                    "price": 7200,
                    "tax": 0
                }
            ],
            "shipping_address": {
                "line1": "Av. Las Condes 11049, Las Condes",
                "city": "Chile",
                "country_code": "CL",
                "phone": "+56956821215",
                "type": "HOME_OR_WORK",
                "recipient_name": "Alejandro Rivero "
            }
        },
        "amount": {
            "currency": "CLP",
            "total": 1000,
            "details": {
                "subtotal": 1000,
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
            "document_number": "371119582",
            "country": "CL",
            "full_name": "Jhon Doe",
            "email": "dummy@gmail.com"
        },
        "payment_method": "QUICKPAY_CREDIT"
    },
    "links": [
        {
            "href": "https://api.qa.peinau.fif.tech/checkout/payments/5c0599e3ca2e140015a77689",
            "rel": "self",
            "method": "GET"
        },
        {
            "href": "https://api.qa.peinau.fif.tech/checkout/payments/gateways/quickpay/credit/5c0599e3ca2e140015a77689/pay",
            "rel": "approval_url",
            "method": "REDIRECT"
        },
        {
            "href": "https://api.qa.peinau.fif.tech/checkout/payments/5c0599e3ca2e140015a77689/edit",
            "rel": "update_url",
            "method": "PUT"
        },
        {
            "href": "https://api.qa.peinau.fif.tech/checkout/payments/gateways/quickpay/credit/5c0599e3ca2e140015a77689/void",
            "rel": "void_method",
            "method": "POST"
        },
        {
            "href": "https://api.qa.peinau.fif.tech/checkout/payments/gateways/quickpay/credit/5c0599e3ca2e140015a77689/refund",
            "rel": "refund_method",
            "method": "POST"
        },
        {
            "href": "https://api.qa.peinau.fif.tech/checkout/payments/gateways/quickpay/credit/5c0599e3ca2e140015a77689/silent",
            "rel": "silent_charge",
            "method": "POST"
        },
        {
            "href": "https://api.qa.peinau.fif.tech/checkout/payments/gateways/quickpay/credit/5c0599e3ca2e140015a77689/installments",
            "rel": "query_installments",
            "method": "GET"
        },
        {
            "href": "https://api.qa.peinau.fif.tech/checkout/payments/gateways/quickpay/credit/5c0599e3ca2e140015a77689/checkBalance",
            "rel": "check_balance",
            "method": "GET"
        },
        {
            "href": "https://api.qa.peinau.fif.tech/checkout/payments/gateways/quickpay/credit/5c0599e3ca2e140015a77689/confirm",
            "rel": "confirm_authorization",
            "method": "POST"
        },
        {
            "href": "https://api.qa.peinau.fif.tech/checkout/payments/IP-15438709476584211",
            "rel": "self_by_gateway_order",
            "method": "GET"
        }
    ],
    "update_time": "2018-12-03T21:02:27.658Z",
    "create_time": "2018-12-03T21:02:27.658Z",
    "invoice_number": "IP-15438709476584211",
    "state": "created",
    "intent": "sale",
    "id": "5c0599e3ca2e140015a77689"
}
```

Obtendrás los Links:

- **self**: desde esta URL puedes consultar la información de pago.
- **self_by_gateway_order**: desde esta URL puedes consultar la información de pago usando el gateway_order.
- **query_installments**: este endpoint se usa para consultar las cuotas de la tarjeta. [ejemplo](quickpay-query-installments.md)
- **check_balance**: este endpoint sirve para consultar si la tarjeta tiene saldo para la compra. [ejemplo](quickpay-check-balance.md)
- **silent_charge**: este endpoint se usa para aplicar la pre-autorización. [ejemplo](quickpay-authorization.md)
- **confirm_authorization**: este endpoint se usa para confirmar la pre-autorización. [ejemplo](quickpay-confirm.md)
- **void_method**: este endpoint sirve para reversar la compra. [ejemplo](quickpay-void.md)
- **refund_method**: este endpoint sirve para anular la compra. [ejemplo](quickpay-refund.md)
