## Ejemplo petición de confirm_authorization:
Según lo devuelto en la creación de la intención de pago, la llamada a la confirmación de la operación previamente autorizada se realiza mediante una llamada POST enviando el access_token previamente obtenido con la Api Single Sign On.

Si no envas nada en el request, Quickpay Connect, confirmará tu orden por el monto original con el que pre autorizaste. En caso necesites confirmar tu pre autorización (pago en estado "authorized") con un monto distinto, debes enviar los siguientes 3 campos: total_amount, tax y subtotal. **Sólo las órdenes de pago en estado authorized podrán ser confirmados.**

Ejemplo en el que se envían los mismos valores que la pre autorización.

```
{
  total_amount: 100,
  tax: 0,
  subtotal: 100,
} 
 
```
 
A continuación se presenta ejemplo de un JSON de respuesta obtenido al confirmar una transacción a través de la API RESTful de checkout:

```
{
    "_id": "5d03b77314c196001682b02a",
    "application": "5ae7359a6a3635000fafbc4c",
    "gateway": {
        "resume": {
            "_id": "5d03b815e30f18001643ec44",
            "card_information": {
                "type": "CMR CLASICA"
            },
            "card_number": {
                "pan_last4": "9299",
                "pan_first6": "627180"
            },
            "authorizations": {
                "code": "168817670307"
            },
            "transaction": {
                "gateway_id": "3519472",
                "type": "CREDIT",
                "date": "2019-06-14T15:07:01.545Z",
                "currency": "CLP",
                "buy_order": "IP-15605246596842971",
                "amount": 100,
                "installments_number": 1
            },
            "response": {
                "code": 200
            }
        },
        "creditAuthorization": {
            "merchTxnId": "IP-15605246596842971-1560524820345",
            "responseCode": 200,
            "firstBuy": null,
            "totalPoints": 180,
            "pointsGained": 0,
            "installmentDetails": {
                "interestRate": 0,
                "nextPaymentDate": "2019-06-14",
                "deferred": 0,
                "installmentAmount": 100,
                "installments": 1
            },
            "price": {
                "price": {
                    "total": 100,
                    "tax": 0,
                    "amount": 100
                },
                "currency": "CLP"
            },
            "authorizationCode": "168817670307",
            "qpTxnId": 3519473,
            "type": "CardAuthorizationResponse"
        },
        "authorization": {
            "type": "PreAuthorizationResponse",
            "qpTxnId": 3519472,
            "preAuthorizationCode": "168817670307",
            "price": {
                "currency": "CLP",
                "price": {
                    "amount": 100,
                    "tax": 0,
                    "total": 100
                }
            },
            "installmentDetails": {
                "installments": 1,
                "installmentAmount": 100,
                "deferred": 0,
                "nextPaymentDate": "2019-06-14",
                "interestRate": 0
            },
            "pointsGained": 0,
            "totalPoints": 180,
            "firstBuy": null,
            "responseCode": 200,
            "qpCardId": "1111317149691298",
            "panFirst6": "627180",
            "panLast4": "9299",
            "cardType": "CMR CLASICA",
            "installments": "1"
        }
    },
    "purchase_order": {
        "purchase_order_id": "048375849305",
        "purchase_order_date": "2018-12-03T00:00:00-05:00"
    },
    "additional_attributes": {
        "capture_token": "bdca7224-6cf6-47e2-bc28-58bb06e1be52",
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
        "gateway_order": "IP-15605246596842971",
        "reference_id": null,
        "description": "Transaction in app 789156083925170982900platform  QPAY id 0dfbb32c-2234-46e5-9e92-561511c00623",
        "soft_descriptor": "id 0dfbb32c-2234-46e5-9e92-561511c00623",
        "amount": {
            "currency": "CLP",
            "total": 100,
            "details": {
                "subtotal": 100,
                "tax": 0,
                "shipping": 0,
                "shipping_discount": 0
            }
        },
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
                "recipient_name": "Alejandro Rivero "
            }
        }
    },
    "payer": {
        "payer_info": {
            "email": "dummy@gmail.com",
            "full_name": "Alejandro Rivero",
            "country": "CL",
            "document_number": "177694886",
            "document_type": "RUT",
            "is_guest": "true"
        },
        "payment_method": "QUICKPAY_CREDIT"
    },
    "links": [
        {
            "href": "https://api.qa.peinau.fif.tech/checkout/payments/5d03b77314c196001682b02a",
            "rel": "self",
            "method": "GET"
        },
        {
            "href": "https://api.qa.peinau.fif.tech/checkout/payments/gateways/quickpay/credit/5d03b77314c196001682b02a/pay",
            "rel": "approval_url",
            "method": "REDIRECT"
        },
        {
            "href": "https://api.qa.peinau.fif.tech/checkout/payments/5d03b77314c196001682b02a/edit",
            "rel": "update_url",
            "method": "PUT"
        },
        {
            "href": "https://api.qa.peinau.fif.tech/checkout/payments/gateways/quickpay/credit/5d03b77314c196001682b02a/void",
            "rel": "void_method",
            "method": "POST"
        },
        {
            "href": "https://api.qa.peinau.fif.tech/checkout/payments/gateways/quickpay/credit/5d03b77314c196001682b02a/refund",
            "rel": "refund_method",
            "method": "POST"
        },
        {
            "href": "https://api.qa.peinau.fif.tech/checkout/payments/gateways/quickpay/credit/5d03b77314c196001682b02a/silent",
            "rel": "silent_charge",
            "method": "POST"
        },
        {
            "href": "https://api.qa.peinau.fif.tech/checkout/payments/gateways/quickpay/credit/5d03b77314c196001682b02a/installments",
            "rel": "query_installments",
            "method": "GET"
        },
        {
            "href": "https://api.qa.peinau.fif.tech/checkout/payments/gateways/quickpay/credit/5d03b77314c196001682b02a/checkBalance",
            "rel": "check_balance",
            "method": "GET"
        },
        {
            "href": "https://api.qa.peinau.fif.tech/checkout/payments/gateways/quickpay/credit/5d03b77314c196001682b02a/confirm",
            "rel": "confirm_authorization",
            "method": "POST"
        }
    ],
    "update_time": "2019-06-14T15:07:01.546Z",
    "create_time": "2019-06-14T15:04:19.684Z",
    "invoice_number": "IP-15605246596842971",
    "state": "paid",
    "intent": "sale",
    "id": "5d03b77314c196001682b02a"
}
```

> **Importante** Podrás ver el detalle de la autorización en el campo **gateway.authorization** y el de la confirmación en **gateway.creditAuthorization**.
