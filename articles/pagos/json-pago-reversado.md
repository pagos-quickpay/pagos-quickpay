```
{
    "_id": "5be35e188cd94e0034c544c6",
    "expiration_date": "2018-11-07T21:55:16.722Z",
    "application": "5af0799cd1aa8e000f9de4ca",
    "gateway": {
        "statusCode": 200,
        "message": "successful reversal",
        "code": "SUCCESSFUL_REVERSAL",
        "txnResponse": {
            "qpTxnId": 2034518
        }
    },
    "redirect_urls": {
        "return_url": "http://www.tottus.cl/tottus/",
        "cancel_url": "https://www.sodimac.cl/sodimac-cl/"
    },
    "transaction": {
        "gateway_order": "IP-15416274166835781",
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
            "total": 2990,
            "details": {
                "subtotal": 300,
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
            "href": "https://api.sandbox.connect.fif.tech/checkout/payments/5be35e188cd94e0034c544c6",
            "rel": "self",
            "method": "GET"
        },
        {
            "href": "https://api.sandbox.connect.fif.tech/checkout/payments/gateways/pagoinapp/credit/5be35e188cd94e0034c544c6/pay",
            "rel": "approval_url",
            "method": "REDIRECT"
        },
        {
            "href": "https://api.sandbox.connect.fif.tech/checkout/payments/5be35e188cd94e0034c544c6/edit",
            "rel": "update_url",
            "method": "PUT"
        }
    ],
    "update_time": "2018-11-07T21:51:14.405Z",
    "create_time": "2018-11-07T21:50:16.683Z",
    "invoice_number": "IP-15416274166835781",
    "state": "reversed",
    "intent": "sale",
    "id": "5be35e188cd94e0034c544c6"
}```
