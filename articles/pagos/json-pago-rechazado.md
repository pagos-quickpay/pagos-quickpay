```
{
    "_id": "5be432acce01180015ca6319",
    "expiration_date": "2018-11-08T12:58:16.948Z",
    "application": "5af0799cd1aa8e000f9de4ca",
    "gateway": {
        "msgType": "PagoInAppResponse",
        "responseCode": 1,
        "responseDescription": "NO_FUNDS",
        "UUID": "8084e7ca-ae5c-486a-ae3c-417c349dfd53",
        "close": false,
        "transactionId": "8084e7ca-ae5c-486a-ae3c-417c349dfd53"
    },
    "redirect_urls": {
        "return_url": "http://www.tottus.cl/tottus/",
        "cancel_url": "https://www.sodimac.cl/sodimac-cl/"
    },
    "transaction": {
        "gateway_order": "IP-15416818369072891",
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
            "document_number": "369086197",
            "document_type": "RUT"
        },
        "payment_method": "PAGOINAPP_CREDIT"
    },
    "links": [
        {
            "href": "https://api.sandbox.connect.fif.tech/checkout/payments/5be432acce01180015ca6319",
            "rel": "self",
            "method": "GET"
        },
        {
            "href": "https://api.sandbox.connect.fif.tech/checkout/payments/gateways/pagoinapp/credit/5be432acce01180015ca6319/pay",
            "rel": "approval_url",
            "method": "REDIRECT"
        },
        {
            "href": "https://api.sandbox.connect.fif.tech/checkout/payments/5be432acce01180015ca6319/edit",
            "rel": "update_url",
            "method": "PUT"
        }
    ],
    "update_time": "2018-11-08T12:57:59.940Z",
    "create_time": "2018-11-08T12:57:16.907Z",
    "invoice_number": "IP-15416818369072891",
    "state": "rejected",
    "intent": "sale",
    "id": "5be432acce01180015ca6319"
}
```
