```
{
    "_id": "5be435bd8cd94e0034c544d1",
    "expiration_date": "2018-11-08T13:11:21.323Z",
    "application": "5af0799cd1aa8e000f9de4ca",
    "gateway": {
        "msgType": "PagoInAppResponse",
        "responseCode": 0,
        "responseDescription": "success",
        "UUID": "ca0368bb-6b89-4d47-b14d-2d3221d5984d",
        "close": true,
        "transactionId": "ca0368bb-6b89-4d47-b14d-2d3221d5984d",
        "txnDetails": {
            "qpTxnId": 2034524,
            "accountLast4": "1434",
            "authorizationCode": "168817595910",
            "status": "success"
        },
        "resume": {
            "response": {
                "code": 0
            },
            "transaction": {
                "installments_number": 0,
                "amount": 300,
                "buy_order": "IP-15416826212839081",
                "currency": "CLP",
                "date": "2018-11-08T13:11:09.108Z",
                "type": "CREDIT",
                "gateway_id": "ca0368bb-6b89-4d47-b14d-2d3221d5984d"
            },
            "authorizations": {
                "code": "168817595910"
            },
            "card_number": {
                "pan_last4": "1434"
            },
            "_id": "5be435ed8cd94e0034c544d2"
        }
    },
    "redirect_urls": {
        "return_url": "http://www.tottus.cl/tottus/",
        "cancel_url": "https://www.sodimac.cl/sodimac-cl/"
    },
    "transaction": {
        "gateway_order": "IP-15416826212839081",
        "description": "Compra COPEC Chesterton",
        "soft_descriptor": "COPEC-PAGO-CLICK",
        "item_list": {
            "shipping_method": "DIGITAL",
            "items": [
                {
                    "thumbnail": "http://portal.test.peinau.fif.tech/bundles/app/css/images/e-commerce-demo/product-icon.png",
                    "sku": "GASOLINA",
                    "name": "Gas. 93",
                    "description": "Gasolina 93, 45lts",
                    "quantity": 1,
                    "price": 400,
                    "tax": 0,
                    "_id": "5a7a14343df88b000fdac92a"
                },
                {
                    "thumbnail": "http://portal.test.peinau.fif.tech/bundles/app/css/images/e-commerce-demo/product-icon.png",
                    "sku": "DESCLIP",
                    "name": "Desc Socio",
                    "description": "Descuento Socio",
                    "quantity": 1,
                    "price": -50,
                    "tax": 0,
                    "_id": "5a7a14343df88b000fdac929"
                },
                {
                    "thumbnail": "http://portal.test.peinau.fif.tech/bundles/app/css/images/e-commerce-demo/product-icon.png",
                    "sku": "DESGASO93",
                    "name": "Desc Falabella",
                    "description": "Destalle Descuento Falabella",
                    "quantity": 1,
                    "price": -50,
                    "tax": 0,
                    "_id": "5a7a14343df88b000fdac928"
                }
            ],
            "shipping_address": {
                "line1": "Dirección Sucursal Matriz Copec",
                "city": "Santiago",
                "country_code": "CL",
                "phone": "+56 9 8762 1244",
                "type": "HOME_OR_WORK",
                "recipient_name": "Jhon Doe Son"
            }
        },
        "amount": {
            "currency": "CLP",
            "total": 300,
            "details": {
                "subtotal": 400,
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
        "payment_method": "PAGOINAPP_CREDIT"
    },
    "links": [
        {
            "href": "https://api.sandbox.connect.fif.tech/checkout/payments/5be435bd8cd94e0034c544d1",
            "rel": "self",
            "method": "GET"
        },
        {
            "href": "https://api.sandbox.connect.fif.tech/checkout/payments/gateways/pagoinapp/credit/5be435bd8cd94e0034c544d1/pay",
            "rel": "approval_url",
            "method": "REDIRECT"
        },
        {
            "href": "https://api.sandbox.connect.fif.tech/checkout/payments/5be435bd8cd94e0034c544d1/edit",
            "rel": "update_url",
            "method": "PUT"
        }
    ],
    "update_time": "2018-11-08T13:11:09.110Z",
    "create_time": "2018-11-08T13:10:21.283Z",
    "invoice_number": "IP-15416826212839081",
    "state": "paid",
    "intent": "sale",
    "id": "5be435bd8cd94e0034c544d1"
}
```
