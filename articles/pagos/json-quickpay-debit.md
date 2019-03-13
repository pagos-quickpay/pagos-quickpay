## Ejemplo petición payment_method": "QUICKPAY_DEBIT"

```
curl -X POST \
  https://api.sandbox.connect.fif.tech/checkout/payments \
  -H 'authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJwcmltYXJ5c2lkIjoiMjhhZGI5OTktN2EyZS03MGI4LWMwOTItZTRjMTZhOWU5ZTBhIiwidW5pcXVlX25hbWUiOiJUb2lwYXRvLmNvbSIsImdyb3Vwc2lkIjoiQVBQTCIsImlzcyI6IkZhbGFiZWxsYSIsImF1ZCI6IldlYiIsInR5cGUiOiJCZWFyZXIiLCJzY29wZSI6W10sImlhdCI6MTUxMzE3Nzk1OCwiZXhwIjoxNTEzMTc4ODU4fQ.OYBksNEvNBU012fJt4IhUnQ5g0szPXPmivD2GvprLczjbG6Pd7HeSyWddSCVOAwAXfycNMzwn0nb_6VdYMqbSzE3T9Bu0Oqzih4b_BfLLb4EwpRQ3L0ObFNkJTI2hfIMUNJQ5ohT8b2yR-1SiehAUd0Tlkb3zrh2aDP9AYVZGqkjLdnwQOpBtXVs6VmntXnb3_MklOU7U0BylB1kVG40t9qfSxf79DYTcr3JWs6LdCFDThkudMZtJfnjYsOoqt--Iv8BzhCU7Eft1Isf2Qfqn_1-p778E7r4yQY1GREuAsXPNfnnHxi7gOVVQ1owq1aekqt4m4ML-VLow8pUx5duYw' \
  -H 'content-type: application/json' \
  -d ' {
  "intent": "sale",
  "transaction": {
    "reference_id": "OD0000233",
    "description": "Transaction detailed description",
    "soft_descriptor": "Transaction Short description",
    "associate_promotion": "PRUEBA",
    "receipt_type": "boleta",
    "with_discount_coupon": "false",
    "amount": {
      "currency": "CLP",
      "total": 1000,
      "details": {
        "subtotal": 1000,
        "tax": 0,
        "discount_percentage": "10",
        "shipping": 0,
        "shipping_discount": 0
      }
    },
    "item_list": {
      "shipping_address": {
        "line1": "General Carol Urzua 1020, Depto 102A",
        "city": "Santiago",
        "country_code": "CL",
        "phone": "+56 9 8762 1244",
        "type": "HOME_OR_WORK",
        "recipient_name": "Jhon Doe Son"
      },
      "shipping_method": "DIGITAL",
      "items": [
        {
          "thumbnail": "http://portal.sandbox.connect.fif.tech/bundles/app/css/images/e-commerce-demo/product-icon.png",
          "sku": "TRK345-2",
          "category": "Viaje Intercontinental",
          "name": "Flight 2344",
          "description": "Flight SCL - ONT",
          "quantity": 1,
          "price": 500,
          "tax": 0
        }
      ]
    }
  },
  "travel": {
    "complete_route": "SCL-JPN",
    "departure_datetime": "11:34",
    "journey_type": "SoloIda",
    "passengers": [
      {
        "first_name": "Juan",
        "last_name": "Perez",
        "phone": "987987987",
        "email": "juanitoperez@gmail.com",
        "document_id": "876123",
        "document_type": "DNI",
        "category": "STATUS",
        "country": "CL",
        "type": "Type"
      }
    ]
  },
  "redirect_urls": {
    "return_url": "http://portal.sandbox.connect.fif.tech",
    "cancel_url": "http://portal.sandbox.connect.fif.tech"
  },
  "additional_attributes": {
    "wedding_code": "987654321",
    "customer_registration_days": "2014-10-15T00:00:00-05:00",
    "first_purchase_days": "901820",
    "installments_offer": [
      "1",
      "3",
      "6"
    ],
    "installments_without_interest": [
      "3"
    ],
    "default_installment_number": "1",
    "default_deferred_month": "0",
    "is_deferred_capture": "false",
    "last_purchase_days": "20",
    "customer_purchases_number": "3",
    "average_purchases_amount": "1233",
    "origin_phone_number": "987987987",
    "copy_paste_email": "false",
    "email_confirmed": "true",
    "changed_register": "false",
    "days_change_register": "5",
    "phone_confirmed": "true",
    "seller_name": "Armando Guerra",
    "modified_order": "false",
    "is_no_food": "true",
    "insuranceCode": "1234567890",
    "insuranceName": "HDI"
  },
  "shipping_list": {
    "shipping": {
      "line1": "Nueva York 54",
      "city": "Santiago",
      "state": "RM",
      "postal_code": "80000",
      "country": "CL",
      "commune": "SANTIAGO",
      "county": "RM",
      "document_type": "CEDULA_DE_CIUDADANIA",
      "document_number": "10321050",
      "first_name": "Andres",
      "last_name": "Roa",
      "phone": "56987861255",
      "store_id": "Nueva York",
      "date": "2016-05-31T00:00:00-03:00",
      "pick_up_type": "TITULAR",
      "type": "RETIRO_TIENDA",
      "shipping_way": "Mail",
      "courier_name": "Falabella"
    }
  },
  "purchase_order": {
    "purchase_order_id": "00536155295217",
    "purchase_order_date": "2018-09-05T00:00:00-05:00"
  },
  "billing_address": {
    "address": "Moneda",
    "city": "Santaigo",
    "state": "RM",
    "postal_code": "80000",
    "country": "CL",
    "commune": "SANTIAGO",
    "county": "RM"
  },
  "payer": {
    "payer_info": {
      "email": "jhondoe@gmail.com",
      "full_name": "Jhon Doe",
      "first_name": "Jhon",
      "last_name": "Doe",
      "country": "CL",
      "document_number": "40820867K",
      "document_type": "RUT",
      "qp_user_id": "",
      "phone": "56987861255",
      "is_guest": "true",
      "gender": "Male",
      "age": "55",
      "session_id": "12345qwrewrasfaeqrew",
      "session_attempt_count": "1",
      "taxpayer_identity": "2343243242"
    },
    "payment_method": "QUICKPAY_DEBIT"
  }
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
 
 
