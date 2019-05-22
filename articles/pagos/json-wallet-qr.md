## Ejemplo petición payment_method": "WALLET_QR"

```
curl -X POST \
  https://api.qa.peinau.fif.tech/checkout/payments \
  -H 'authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJwcmltYXJ5c2lkIjoiMjhhZGI5OTktN2EyZS03MGI4LWMwOTItZTRjMTZhOWU5ZTBhIiwidW5pcXVlX25hbWUiOiJUb2lwYXRvLmNvbSIsImdyb3Vwc2lkIjoiQVBQTCIsImlzcyI6IkZhbGFiZWxsYSIsImF1ZCI6IldlYiIsInR5cGUiOiJCZWFyZXIiLCJzY29wZSI6W10sImlhdCI6MTUxMzE3Nzk1OCwiZXhwIjoxNTEzMTc4ODU4fQ.OYBksNEvNBU012fJt4IhUnQ5g0szPXPmivD2GvprLczjbG6Pd7HeSyWddSCVOAwAXfycNMzwn0nb_6VdYMqbSzE3T9Bu0Oqzih4b_BfLLb4EwpRQ3L0ObFNkJTI2hfIMUNJQ5ohT8b2yR-1SiehAUd0Tlkb3zrh2aDP9AYVZGqkjLdnwQOpBtXVs6VmntXnb3_MklOU7U0BylB1kVG40t9qfSxf79DYTcr3JWs6LdCFDThkudMZtJfnjYsOoqt--Iv8BzhCU7Eft1Isf2Qfqn_1-p778E7r4yQY1GREuAsXPNfnnHxi7gOVVQ1owq1aekqt4m4ML-VLow8pUx5duYw' \
  -H 'content-type: application/json' \
  -d '{
  "intent": "sale",
  "payer": {
    "payer_info": {
      "email": "pperez@gmail.com",
      "full_name": "Pedro Perez",
      "country": "CL",
      "document_number": "371119582",
      "document_type": "RUT"
    },
    "payment_method": "WALLET_QR"
  },
  "transaction": {
    "gateway_order": "identificador_unico comercio (max 12 caracteres)",
    "description": "Compra en Comercio X",
    "soft_descriptor": "COMERCIO",
    "item_list": {
      "shipping_method": "DIGITAL",
      "items": [
        {
          "thumbnail": "http://portal.test.peinau.fif.tech/bundles/app/css/images/e-commerce-demo/product-icon.png",
          "sku": "123456789",
          "name": "PRODUCTO X",
          "description": "DESCRIPCON X",
          "quantity": 1,
          "price": 30000,
          "tax": 0,
          "_id": "5a7a14343df88b000fdac92a"
        },
        {
          "thumbnail": "http://portal.test.peinau.fif.tech/bundles/app/css/images/e-commerce-demo/product-icon.png",
          "sku": "DESCLIP",
          "name": "Desc Socio",
          "description": "Descuento Socio",
          "quantity": 1,
          "price": -1500,
          "tax": 0,
          "_id": "5a7a14343df88b000fdac929"
        },
        {
          "thumbnail": "http://portal.test.peinau.fif.tech/bundles/app/css/images/e-commerce-demo/product-icon.png",
          "sku": "DESGASO93",
          "name": "Desc Falabella",
          "description": "Destalle Descuento Falabella",
          "quantity": 1,
          "price": -2000,
          "tax": 0,
          "_id": "5a7a14343df88b000fdac928"
        }
      ],
      "shipping_address": {
        "line1": Moneda 970",
        "city": "Santiago",
        "country_code": "CL",
        "phone": "+56 9 1234 1234",
        "type": "HOME_OR_WORK",
        "recipient_name": "Jhon Doe Son"
      }
    },
    "amount": {
      "currency": "CLP",
      "total": 26500,
      "details": {
        "subtotal": 26500,
        "tax": 0,
        "shipping": 0,
        "shipping_discount": 0
      }
    }
  },
  "redirect_urls": {
    "return_url": "http://portal.sandbox.connect.fif.tech",
    "cancel_url": "http://portal.sandbox.connect.fif.tech"
  },
  "additional_attributes": {
      "promotions": [
        {
          "type": "CMR",
          "amount": 10000,
          "currency": "CLP",
        }
      ],
      "installments_offer":[
         "1",
         "3",
         "6"
      ],
      "installments_without_interest":[  
         "3"
      ],
      "default_installment_number":"1",
      "default_deferred_month":"3",
  }
}'
 ```
 
A continuación se presenta ejemplo de un JSON de respuesta obtenido al crear una intención de pago a través de la API RESTful de checkout:

```
{
    "application": "5af0799cd1aa8e000f9de4ca",
    "_id": "5b6121d4d28fc400163111d6",
    "redirect_urls": {
        "return_url": "http://portal.sandbox.connect.fif.tech",
        "cancel_url": "http://portal.sandbox.connect.fif.tech"
    },
    "transaction": {
        "gateway_order": "INPA-1533092308183",
        "description": "Compra en Comercio X",
        "soft_descriptor": "PRODUCTO X",
        "item_list": {
            "shipping_method": "DIGITAL",
            "items": [
                {
                    "thumbnail": "http://portal.test.peinau.fif.tech/bundles/app/css/images/e-commerce-demo/product-icon.png",
                    "sku": "GASOLINA",
                    "name": "Gas. 93",
                    "description": "Gasolina 93, 45lts",
                    "quantity": 1,
                    "price": 30000,
                    "tax": 0,
                    "_id": "5a7a14343df88b000fdac92a"
                },
                {
                    "thumbnail": "http://portal.test.peinau.fif.tech/bundles/app/css/images/e-commerce-demo/product-icon.png",
                    "sku": "DESCLIP",
                    "name": "Desc Socio",
                    "description": "Descuento Socio",
                    "quantity": 1,
                    "price": -1500,
                    "tax": 0,
                    "_id": "5a7a14343df88b000fdac929"
                },
                {
                    "thumbnail": "http://portal.test.peinau.fif.tech/bundles/app/css/images/e-commerce-demo/product-icon.png",
                    "sku": "DESGASO93",
                    "name": "Desc Falabella",
                    "description": "Destalle Descuento Falabella",
                    "quantity": 1,
                    "price": -2000,
                    "tax": 0,
                    "_id": "5a7a14343df88b000fdac928"
                }
            ],
            "shipping_address": {
                "line1": "Moneda 970",
                "city": "Santiago",
                "country_code": "CL",
                "phone": "+56 9 1234 1234",
                "type": "HOME_OR_WORK",
                "recipient_name": "Jhon Doe Son"
            }
        },
        "amount": {
            "currency": "CLP",
            "total": 26500,
            "details": {
                "subtotal": 26500,
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
        "payment_method": "PAGOINAPP_CREDIT"
    },
    "links": [
        {
            "href": "https://api.sandbox.connect.fif.tech/checkout/payments/5b6121d4d28fc400163111d6",
            "rel": "self",
            "method": "GET"
        },
        {
            "href": "https://api.sandbox.connect.fif.tech/checkout/payments/gateways/pagoinapp/credit/5b6121d4d28fc400163111d6/pay",
            "rel": "approval_url",
            "method": "REDIRECT"
        },
        {
            "href": "https://api.sandbox.connect.fif.tech/checkout/payments/5b6121d4d28fc400163111d6/edit",
            "rel": "update_url",
            "method": "PUT"
        },
        {
            "href": "https://api.sandbox.connect.fif.tech/checkout/payments/INPA-1533092308183",
            "rel": "self_by_gateway_order",
            "method": "GET"
        }
    ],
    "update_time": "2018-08-01T02:58:28.183Z",
    "create_time": "2018-08-01T02:58:28.183Z",
    "invoice_number": "INPA-1533092308183",
    "state": "created",
    "intent": "sale",
    "id": "5b6121d4d28fc400163111d6"
}
```
 
 Posibles resultados de la transacción
 
 - [Json ejemplo Pago Exitoso](json-pago-exitoso.md)
 - [Json ejemplo respuesta por NO cliente](json-no-cliente.md)
 - [Json ejemplo Pago Rechazado](json-pago-rechazado.md)
 - [Json ejemplo Pago Expirado](json-pago-expirado.md)
 - [Json ejemplo Pago Reversado](json-pago-reversado.md)
