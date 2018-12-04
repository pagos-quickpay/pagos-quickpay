## Ejemplo petición de check balance:

Para saber si la tarjeta tiene saldo suficiente se debe invocar el endpoint rel: “check_balance”
 
A continuación se presenta ejemplo de un JSON de respuesta obtenido al crear una intención de pago a través de la API RESTful de checkout:

```
{
    "gateway": {
        "balance": {
            "status": "0",
            "sufficient": true
        }
    },
    "_id": "5c05a169ca2e140015a77698",
    "application": "5af350553dbed900146c5945",
    "additional_attributes": {
        "capture_token": "b3718ffc-e542-416d-a02b-ddf9afb2a007",
        "installments_offer": [
            "1",
            "2",
            "3",
            "4"
        ],
        "installments_without_interest": [
            "2"
        ],
        "default_installment_number": "1",
        "default_deferred_month": "0",
        "is_deferred_capture": "true"
    },
    "redirect_urls": {
        "return_url": "https://www.falabella.com",
        "cancel_url": "https://www.google.com"
    },
    "transaction": {
        "gateway_order": "IP-15438728737716541",
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
                "recipient_name": "Jhon Doe"
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
            "email": "dummy@gmail.com",
            "full_name": "Jhon Doe",
            "country": "CL",
            "document_number": "371119582",
            "document_type": "RUT",
            "is_guest": "true"
        },
        "payment_method": "QUICKPAY_CREDIT"
    },
    "links": [
        {
            "href": "https://api.qa.peinau.fif.tech/checkout/payments/5c05a169ca2e140015a77698",
            "rel": "self",
            "method": "GET"
        },
        {
            "href": "https://api.qa.peinau.fif.tech/checkout/payments/gateways/quickpay/credit/5c05a169ca2e140015a77698/pay",
            "rel": "approval_url",
            "method": "REDIRECT"
        },
        {
            "href": "https://api.qa.peinau.fif.tech/checkout/payments/5c05a169ca2e140015a77698/edit",
            "rel": "update_url",
            "method": "PUT"
        },
        {
            "href": "https://api.qa.peinau.fif.tech/checkout/payments/gateways/quickpay/credit/5c05a169ca2e140015a77698/void",
            "rel": "void_method",
            "method": "POST"
        },
        {
            "href": "https://api.qa.peinau.fif.tech/checkout/payments/gateways/quickpay/credit/5c05a169ca2e140015a77698/refund",
            "rel": "refund_method",
            "method": "POST"
        },
        {
            "href": "https://api.qa.peinau.fif.tech/checkout/payments/gateways/quickpay/credit/5c05a169ca2e140015a77698/silent",
            "rel": "silent_charge",
            "method": "POST"
        },
        {
            "href": "https://api.qa.peinau.fif.tech/checkout/payments/gateways/quickpay/credit/5c05a169ca2e140015a77698/installments",
            "rel": "query_installments",
            "method": "GET"
        },
        {
            "href": "https://api.qa.peinau.fif.tech/checkout/payments/gateways/quickpay/credit/5c05a169ca2e140015a77698/checkBalance",
            "rel": "check_balance",
            "method": "GET"
        }
    ],
    "update_time": "2018-12-03T21:34:48.302Z",
    "create_time": "2018-12-03T21:34:33.771Z",
    "invoice_number": "IP-15438728737716541",
    "state": "created",
    "intent": "sale",
    "id": "5c05a169ca2e140015a77698"
}
```


