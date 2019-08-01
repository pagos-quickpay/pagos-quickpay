## Ejemplo petición de reversa:

Para poder reversar la transacción de débito, de debe hacer una llamada POST a la url **void**. A continuación, un ejemplo:

```
curl -X POST \
  https://api.qa.peinau.fif.tech/checkout/payments/gateways/quickpay/debit/5d430d3c37c100001ce70e67/void \
  -H 'Authorization: Bearer TOKEN_ACCESO' \
  -H 'Cache-Control: no-cache'
```

 
A continuación se presenta ejemplo de un JSON de respuesta obtenido al reversar una intención de pago a través de la API RESTful de checkout:

```
{
    "_id": "5d430d3c37c100001ce70e67",
    "application": "5c8ba010d37626001dc3c794",
    "gateway": {
        "void": {
            "txnResponse": {
                "qpTxnId": 3928804
            },
            "code": "SUCCESSFUL_REVERSAL",
            "message": "successful reversal",
            "statusCode": 200
        },
        "msgType": "DebitResponse",
        "responseCode": 0,
        "responseDescription": "Success",
        "responseSignature": "/4/ej0MfUAMWUdAFX6xm6xzPuS78DTl2aMHSOBmk+KI=",
        "payerUserProfile": {
            "country": "CL",
            "documentType": "RUT",
            "documentId": "8359747K",
            "category": "NORMAL",
            "isEmploye": false
        },
        "logTrackId": "#LGID=da52556d53e63b1d60b9638d00b1e211#MID=007690769#CID=WEB#PYMT=D#DT=RUT#DID=8359747K#",
        "riskEngineFinalResult": "0",
        "qpTxnId": 3928799,
        "authorizationCode": "110364815",
        "resume": {
            "response": {
                "code": 0
            },
            "transaction": {
                "installments_number": 0,
                "amount": 100,
                "buy_order": "IP-15646753882100531",
                "currency": "CLP",
                "date": "2019-08-01T16:03:47.958Z",
                "type": "DEBIT",
                "gateway_id": "3928799"
            },
            "authorizations": {
                "code": "110364815"
            },
            "_id": "5d430d6337c100001ce70e6b"
        }
    },
    "purchase_order": {
        "purchase_order_id": "1231266",
        "purchase_order_date": "2018-09-05T00:00:00-05:00"
    },
    "redirect_urls": {
        "return_url": "http://portal.sandbox.connect.fif.tech",
        "cancel_url": "http://portal.sandbox.connect.fif.tech"
    },
    "transaction": {
        "gateway_order": "IP-15646753882100531",
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
            "total": 100,
            "details": {
                "subtotal": 100,
                "tax": 0,
                "shipping": 0,
                "shipping_discount": 0
            }
        }
    },
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
    "links": [
        {
            "href": "https://api.qa.peinau.fif.tech/checkout/payments/5d430d3c37c100001ce70e67",
            "rel": "self",
            "method": "GET"
        },
        {
            "href": "https://api.qa.peinau.fif.tech/checkout/payments/gateways/quickpay/debit/5d430d3c37c100001ce70e67/pay",
            "rel": "approval_url",
            "method": "REDIRECT"
        },
        {
            "href": "https://api.qa.peinau.fif.tech/checkout/payments/5d430d3c37c100001ce70e67/edit",
            "rel": "update_url",
            "method": "PUT"
        },
        {
            "href": "https://api.qa.peinau.fif.tech/checkout/payments/gateways/quickpay/debit/5d430d3c37c100001ce70e67/void",
            "rel": "void_method",
            "method": "POST"
        },
        {
            "href": "https://api.qa.peinau.fif.tech/checkout/payments/gateways/quickpay/debit/5d430d3c37c100001ce70e67/refund",
            "rel": "refund_method",
            "method": "POST"
        }
    ],
    "update_time": "2019-08-01T16:06:03.680Z",
    "create_time": "2019-08-01T16:03:08.210Z",
    "invoice_number": "IP-15646753882100531",
    "state": "voided",
    "intent": "sale",
    "id": "5d430d3c37c100001ce70e67"
}
```

[Regresar](json-quickpay-debit.md)


