## Ejemplo petición payment_method": "QUICKPAY_DEBIT"

```
curl -X POST \
  https://api.sandbox.connect.fif.tech/checkout/payments \
  -H 'authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJwcmltYXJ5c2lkIjoiMjhhZGI5OTktN2EyZS03MGI4LWMwOTItZTRjMTZhOWU5ZTBhIiwidW5pcXVlX25hbWUiOiJUb2lwYXRvLmNvbSIsImdyb3Vwc2lkIjoiQVBQTCIsImlzcyI6IkZhbGFiZWxsYSIsImF1ZCI6IldlYiIsInR5cGUiOiJCZWFyZXIiLCJzY29wZSI6W10sImlhdCI6MTUxMzE3Nzk1OCwiZXhwIjoxNTEzMTc4ODU4fQ.OYBksNEvNBU012fJt4IhUnQ5g0szPXPmivD2GvprLczjbG6Pd7HeSyWddSCVOAwAXfycNMzwn0nb_6VdYMqbSzE3T9Bu0Oqzih4b_BfLLb4EwpRQ3L0ObFNkJTI2hfIMUNJQ5ohT8b2yR-1SiehAUd0Tlkb3zrh2aDP9AYVZGqkjLdnwQOpBtXVs6VmntXnb3_MklOU7U0BylB1kVG40t9qfSxf79DYTcr3JWs6LdCFDThkudMZtJfnjYsOoqt--Iv8BzhCU7Eft1Isf2Qfqn_1-p778E7r4yQY1GREuAsXPNfnnHxi7gOVVQ1owq1aekqt4m4ML-VLow8pUx5duYw' \
  -H 'content-type: application/json' \
  -d '{
        "intent": "sale",
        "payer": {
          "payer_info": {
              "email": "aroa@gmail.com",
              "full_name": "Andres Roa",
              "country": "CL",
              "document_number": "371119582",
              "document_type": "RUT"
          },
          "payment_method": "QUICKPAY_DEBIT"
        },
        "transaction": {
          "gateway_order": "identificador_unico",
          "description": "Compra comercio x",
          "soft_descriptor": "Compra comercio x",
          "amount": {
            "currency": "CLP",
            "total": 1000,
            "details": {
              "subtotal": 1000,
              "tax": 0,
              "shipping": 0,
              "shipping_discount": 0
            }
          },
          "item_list": {
            "shipping_address": {
                "line1": "Direccion del cliente",
                "city": "Santiago",
                "country_code": "CL",
                "phone": "+56 9 8762 1244",
                "type": "HOME_OR_WORK",
                "recipient_name": "Luisa Perez"
            },
            "shipping_method": "DIGITAL",
            "items": [
              {
                "thumbnail": "http://portal.sandbox.connect.fif.tech/bundles/app/css/images/e-commerce-demo/product-icon.png",
                "sku": "983792642-2",
                "name": "Producto A",
                "description": "Producto A con caracteristicas B",
                "quantity": 2,
                "price": 500,
                "tax": 0
              }
            ]
          }
        },
        "redirect_urls": {
          "return_url": "http://portal.sandbox.connect.fif.tech",
          "cancel_url": "http://portal.sandbox.connect.fif.tech"
        },
        "additional_attributes": {}
      }'
 ```
 
A continuación se presenta ejemplo de un JSON de respuesta obtenido al crear una intención de pago a través de la API RESTful de checkout:

```
{
    "application": "5ae7359a6a3635000fafbc4c",
    "_id": "5b76e5653cecac0015e3de55",
    "redirect_urls": {
        "return_url": "http://portal.sandbox.connect.fif.tech",
        "cancel_url": "http://portal.sandbox.connect.fif.tech"
    },
    "transaction": {
        "gateway_order": "INPA-1534518629615",
        "description": "Compra comercio x",
        "soft_descriptor": "Compra comercio x",
        "item_list": {
            "shipping_method": "DIGITAL",
            "items": [
                {
                    "thumbnail": "http://portal.sandbox.connect.fif.tech/bundles/app/css/images/e-commerce-demo/product-icon.png",
                    "sku": "983792642-2",
                    "name": "Producto A",
                    "description": "Producto A con caracteristicas B",
                    "quantity": 2,
                    "price": 500,
                    "tax": 0
                }
            ],
            "shipping_address": {
                "line1": "Direccion del cliente",
                "city": "Santiago",
                "country_code": "CL",
                "phone": "+56 9 8762 1244",
                "type": "HOME_OR_WORK",
                "recipient_name": "Luisa Perez"
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
            "document_type": "RUT",
            "document_number": "371119582",
            "country": "CL",
            "full_name": "Andres Roa",
            "email": "aroa@gmail.com"
        },
        "payment_method": "QUICKPAY_DEBIT"
    },
    "links": [
        {
            "href": "https://api.qa.peinau.fif.tech/checkout/payments/5b76e5653cecac0015e3de55",
            "rel": "self",
            "method": "GET"
        },
        {
            "href": "https://api.qa.peinau.fif.tech/checkout/payments/gateways/quickpay/debit/5b76e5653cecac0015e3de55/pay",
            "rel": "approval_url",
            "method": "REDIRECT"
        },
        {
            "href": "https://api.qa.peinau.fif.tech/checkout/payments/5b76e5653cecac0015e3de55/edit",
            "rel": "update_url",
            "method": "PUT"
        },
        {
            "href": "https://api.qa.peinau.fif.tech/checkout/payments/INPA-1534518629615",
            "rel": "self_by_gateway_order",
            "method": "GET"
        }
    ],
    "update_time": "2018-08-17T15:10:29.615Z",
    "create_time": "2018-08-17T15:10:29.615Z",
    "invoice_number": "INPA-1534518629615",
    "state": "created",
    "intent": "sale",
    "id": "5b76e5653cecac0015e3de55"
}
```
 
 
