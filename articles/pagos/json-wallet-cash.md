## Ejemplo petición payment_method": "WALLET_CASH"

```
curl -X POST \
  https://api.qa.peinau.fif.tech/checkout/payments \
  -H 'authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJwcmltYXJ5c2lkIjoiMjhhZGI5OTktN2EyZS03MGI4LWMwOTItZTRjMTZhOWU5ZTBhIiwidW5pcXVlX25hbWUiOiJUb2lwYXRvLmNvbSIsImdyb3Vwc2lkIjoiQVBQTCIsImlzcyI6IkZhbGFiZWxsYSIsImF1ZCI6IldlYiIsInR5cGUiOiJCZWFyZXIiLCJzY29wZSI6W10sImlhdCI6MTUxMzE3Nzk1OCwiZXhwIjoxNTEzMTc4ODU4fQ.OYBksNEvNBU012fJt4IhUnQ5g0szPXPmivD2GvprLczjbG6Pd7HeSyWddSCVOAwAXfycNMzwn0nb_6VdYMqbSzE3T9Bu0Oqzih4b_BfLLb4EwpRQ3L0ObFNkJTI2hfIMUNJQ5ohT8b2yR-1SiehAUd0Tlkb3zrh2aDP9AYVZGqkjLdnwQOpBtXVs6VmntXnb3_MklOU7U0BylB1kVG40t9qfSxf79DYTcr3JWs6LdCFDThkudMZtJfnjYsOoqt--Iv8BzhCU7Eft1Isf2Qfqn_1-p778E7r4yQY1GREuAsXPNfnnHxi7gOVVQ1owq1aekqt4m4ML-VLow8pUx5duYw' \
  -H 'content-type: application/json' \
  -d '{
  "intent": "sale",
  "payment_method": "WALLET_CASH",
  "payer": {
    "email": "pperez@gmail.com",
    "full_name": "Pedro Perez",
    "country": "CL",
    "document_number": "371119582",
    "document_type": "RUT"
  },
  "transaction": {
    "purchase_order": "identificador_unico comercio (max 12 caracteres)",
    "description": "Compra en Comercio X",
    "soft_descriptor": "COMERCIO",
    "type": "CASH_IN/CASH_OUT"
    "channel:" "WEB",
    "item_list": {
      "shipping_method": "DIGITAL",
      "items": [
        {
          "sku": "123456789",
          "name": "PRODUCTO X",
          "description": "DESCRIPCON X",
          "quantity": 1,
          "price": 30000,
          "tax": 0
        }
      ]
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
  "additional_attributes": {
      
  }
}'
 ```
 
A continuación se presenta ejemplo de un JSON de respuesta obtenido al crear una intención de pago a través de la API RESTful de checkout:

```
{
    "application": "5af0799cd1aa8e000f9de4ca",
    "_id": "5b6121d4d28fc400163111d6",
    "payment_method": "WALLET_CASH"
    "transaction": {
      "purchase_order": "identificador_unico comercio (max 12 caracteres)",
      "description": "Compra en Comercio X",
      "soft_descriptor": "COMERCIO",
      "type": "CASH_IN/CASH_OUT"
      "channel:" "WEB",
      "item_list": {
        "shipping_method": "DIGITAL",
        "items": [
          {
            "sku": "123456789",
            "name": "PRODUCTO X",
            "description": "DESCRIPCON X",
            "quantity": 1,
            "price": 30000,
            "tax": 0
          }
        ]
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
      "email": "pperez@gmail.com",
      "full_name": "Pedro Perez",
      "country": "CL",
      "document_number": "371119582",
      "document_type": "RUT"
    },
    "links": [
        {
            "href": "https://api.sandbox.connect.fif.tech/checkout/payments/5b6121d4d28fc400163111d6",
            "rel": "self",
            "method": "GET"
        },
        {
            "href": "https://api.sandbox.connect.fif.tech/checkout/payments/{payment_method}/5b6121d4d28fc400163111d6",
            "rel": "confirm",
            "method": "POST"
        },
        {
            "href": "https://api.sandbox.connect.fif.tech/checkout/payments/code/1234ABCD",
            "rel": "self_by_transaction_code",
            "method": "GET"
        }
    ],
    "update_time": "2018-08-01T02:58:28.183Z",
    "create_time": "2018-08-01T02:58:28.183Z",
    "state": "created",
    "intent": "sale",
    "id": "5b6121d4d28fc400163111d6"
}
```
 
 Posibles resultados de la transacción
 
 - [Json ejemplo Pago Exitoso](json-wallet-cash-exitoso.md)
 - [Json ejemplo Pago Rechazado](json-wallet-cash-rechazado.md)
 - [Json ejemplo Pago Expirado](json-wallet-cash-expirado.md) (Por confirmar si es necesario)
