## Ejemplo petición de devolución:

Para saber si la tarjeta tiene saldo suficiente se debe invocar el endpoint rel: “refund_method”. Ejemplo

```
 curl -X POST 'https://api.qa.peinau.fif.tech/checkout/payments/gateways/quickpay/credit/5c0a6b7ed5b963001553865d/refund' \
  -H 'authorization: Bearer REEMPLAZAR AQUI EL ACCESS TOKEN' \
  -H 'content-type: application/json' \
  -d '{
	   "refunded_amount":"1000",
    	"items": [{
      "sku": "117110",
      "quantity": 1
     }]
  }'
```
El campo "items" es opcional.
 
A continuación se presenta ejemplo de un JSON de respuesta obtenido al devolver una intención de pago a través de la API RESTful de checkout:

```
{
    "_id": "5c0a6b7ed5b963001553865d",
    "application": "5b15884a2e3f440015449de3",
    "gateway": {
        "refunds": [
            {
                "refunded_amount": 1000,
                "message": "successful refund",
                "refundResponseCode": 0,
                "refundResponseDescription": "Success",
                "refundCancelationCode": "168817603278",
                "refundTxnId": "2392960"
            }
        ],
        "authorization": {
            "msgType": "CreditResponse",
            "responseCode": 0,
            "responseDescription": "Success",
            "responseSignature": "3bLWvckF7wr0XdLp3cEwoWm/dMtQv/GtrYioeSwXqHY=",
            "payerUserProfile": {
                "country": "CL",
                "documentType": "RUT",
                "documentId": "371119582",
                "category": "Premium",
                "isEmploye": false
            },
            "logTrackId": "#LGID=8eca81174d5a425b5942bc3ab2487385#MID=008598176#CID=WEB#PYMT=C#DT=RUT#DID=371119582#",
            "riskEngineFinalResult": "0",
            "qpTxnId": 2392959,
            "authorizationCodes": {
                "money": "168817603277",
                "points": null
            },
            "amounts": {
                "money": 1000,
                "points": 0,
                "currency": "CLP"
            },
            "installments": 1,
            "installmentAmount": 1000,
            "deferred": 0,
            "nextPaymentDate": "2018-12-07T12:46:22Z",
            "interestRate": 0,
            "userChangedDocument": true,
            "cardExp": null,
            "panFirst6": "445596",
            "panLast4": "1434",
            "txnSuccess": true,
            "qpCardId": null,
            "qpUserId": null
        },
        "resume": {
            "response": {
                "code": 0
            },
            "transaction": {
                "installments_number": 1,
                "amount": 1000,
                "buy_order": "IP-15441867508491071",
                "currency": "CLP",
                "date": "2018-12-07T12:46:26.369Z",
                "type": "CREDIT",
                "gateway_id": "2392959"
            },
            "authorizations": {
                "code": "168817603277"
            },
            "card_number": {
                "pan_first6": "445596",
                "pan_last4": "1434"
            },
            "_id": "5c0a6ba2d5b963001553865f"
        }
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
    "purchase_order": {
        "purchase_order_id": "536155295217",
        "purchase_order_date": "2018-09-05T00:00:00-05:00"
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
        "is_no_food": "true"
    },
    "redirect_urls": {
        "return_url": "http://portal.sandbox.connect.fif.tech",
        "cancel_url": "http://portal.sandbox.connect.fif.tech"
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
    "transaction": {
        "gateway_order": "IP-15441867508491071",
        "reference_id": "OD0000233",
        "description": "Transaction detailed description",
        "soft_descriptor": "Transaction Short description",
        "associated_promotion": "PRUEBA",
        "receipt_type": "boleta",
        "with_discount_coupon": "false",
        "item_list": {
            "shipping_method": "DIGITAL",
            "items": [
                {
                    "thumbnail": "http://portal.sandbox.connect.fif.tech/bundles/app/css/images/e-commerce-demo/product-icon.png",
                    "sku": "TRK345-2",
                    "category": "Viaje Intercontinental",
                    "name": "Flight 2344",
                    "description": "Flight SCL - ONT",
                    "quantity": 2,
                    "price": 500,
                    "tax": 0
                }
            ],
            "shipping_address": {
                "line1": "General Carol Urzua 1020, Depto 102A",
                "city": "Santiago",
                "country_code": "CL",
                "phone": "+56 9 8762 1244",
                "type": "HOME_OR_WORK",
                "recipient_name": "Jhon Doe Son"
            }
        },
        "amount": {
            "currency": "CLP",
            "total": 1000,
            "details": {
                "subtotal": 1000,
                "tax": 0,
                "discount_percentage": 10,
                "shipping": 0,
                "shipping_discount": 0
            }
        }
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
        "payment_method": "QUICKPAY_CREDIT"
    },
    "links": [
        {
            "href": "https://api.qa.peinau.fif.tech/checkout/payments/5c0a6b7ed5b963001553865d",
            "rel": "self",
            "method": "GET"
        },
        {
            "href": "https://api.qa.peinau.fif.tech/checkout/payments/gateways/quickpay/credit/5c0a6b7ed5b963001553865d/pay",
            "rel": "approval_url",
            "method": "REDIRECT"
        },
        {
            "href": "https://api.qa.peinau.fif.tech/checkout/payments/5c0a6b7ed5b963001553865d/edit",
            "rel": "update_url",
            "method": "PUT"
        },
        {
            "href": "https://api.qa.peinau.fif.tech/checkout/payments/gateways/quickpay/credit/5c0a6b7ed5b963001553865d/void",
            "rel": "void_method",
            "method": "POST"
        },
        {
            "href": "https://api.qa.peinau.fif.tech/checkout/payments/gateways/quickpay/credit/5c0a6b7ed5b963001553865d/refund",
            "rel": "refund_method",
            "method": "POST"
        },
        {
            "href": "https://api.qa.peinau.fif.tech/checkout/payments/gateways/quickpay/credit/5c0a6b7ed5b963001553865d/silent",
            "rel": "silent_charge",
            "method": "POST"
        },
        {
            "href": "https://api.qa.peinau.fif.tech/checkout/payments/gateways/quickpay/credit/5c0a6b7ed5b963001553865d/installments",
            "rel": "query_installments",
            "method": "GET"
        },
        {
            "href": "https://api.qa.peinau.fif.tech/checkout/payments/gateways/quickpay/credit/5c0a6b7ed5b963001553865d/checkBalance",
            "rel": "check_balance",
            "method": "GET"
        }
    ],
    "update_time": "2018-12-07T12:46:46.653Z",
    "create_time": "2018-12-07T12:45:50.849Z",
    "invoice_number": "IP-15441867508491071",
    "state": "refunded",
    "intent": "sale",
    "id": "5c0a6b7ed5b963001553865d"
}
```


