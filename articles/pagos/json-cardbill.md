## Ejemplo petición payment_method": "CARDBILL_PAYMENT_DEBIT_BF"

 ```
 {
  "intent": "sale",
  "payer": {
    "payer_info": {
      "email": "jhondoe@gmail.com",
      "full_name": "Jhon Doe",
      "country": "CL",
      "document_number": "371377387",
      "document_type": "RUT"
    },
    "payment_method": "CARDBILL_PAYMENT_DEBIT_BF"
  },
  "transaction": {
    "gateway_order": "123456789",
    "description": "Transaction detailed description",
    "soft_descriptor": "Transaction Short description",
    "amount": {
      "currency": "CLP",
      "total": 1000,
      "details": {
        "subtotal": 1000,
        "tax": 0,
        "shipping": 0,
        "shipping_discount": 0
      }
    },
    "item_list": {
      "shipping_address": {
        "line1": "Moneda 970",
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
          "name": "Flight 2344",
          "description": "Flight SCL - ONT",
          "quantity": 2,
          "price": 500,
          "tax": 0
        }
      ]
    }
  },
  "redirect_urls": {
    "return_url": "http://portal.sandbox.connect.fif.tech",
    "cancel_url": "http://portal.sandbox.connect.fif.tech"
  },
  "additional_attributes": {
    "card_bin": 548740,
    "last_four_digits": "3038"
  }
}
```

A continuación se presenta ejemplo de un JSON de respuesta obtenido al crear una intención de pago a través de la API RESTful de checkout:

```
{
    "application": "5ae7359a6a3635000fafbc4c",
    "_id": "5b622b8ddd053a001662dd5a",
    "additional_attributes": {
        "last_four_digits": "3038",
        "card_bin": 548740
    },
    "redirect_urls": {
        "return_url": "http://portal.sandbox.connect.fif.tech",
        "cancel_url": "http://portal.sandbox.connect.fif.tech"
    },
    "transaction": {
        "gateway_order": "123456789",
        "description": "Transaction detailed description",
        "soft_descriptor": "Transaction Short description",
        "item_list": {
            "shipping_method": "DIGITAL",
            "items": [
                {
                    "thumbnail": "http://portal.sandbox.connect.fif.tech/bundles/app/css/images/e-commerce-demo/product-icon.png",
                    "sku": "TRK345-2",
                    "name": "Flight 2344",
                    "description": "Flight SCL - ONT",
                    "quantity": 2,
                    "price": 500,
                    "tax": 0
                }
            ],
            "shipping_address": {
                "line1": "Moneda 970",
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
                "shipping": 0,
                "shipping_discount": 0
            }
        }
    },
    "payer": {
        "payer_info": {
            "document_type": "RUT",
            "document_number": "371377387",
            "country": "CL",
            "full_name": "Jhon Doe",
            "email": "jhondoe@gmail.com"
        },
        "payment_method": "CARDBILL_PAYMENT_DEBIT_BF"
    },
    "links": [
        {
            "href": "https://api.qa.peinau.fif.tech/checkout/payments/5b622b8ddd053a001662dd5a",
            "rel": "self",
            "method": "GET"
        },
        {
            "href": "https://api.qa.peinau.fif.tech/checkout/payments/gateways/cardbill/payment_debit_bf/5b622b8ddd053a001662dd5a/pay",
            "rel": "approval_url",
            "method": "REDIRECT"
        },
        {
            "href": "https://api.qa.peinau.fif.tech/checkout/payments/5b622b8ddd053a001662dd5a/edit",
            "rel": "update_url",
            "method": "PUT"
        },
        {
            "href": "https://api.qa.peinau.fif.tech/checkout/payments/123456789",
            "rel": "self_by_gateway_order",
            "method": "GET"
        }
    ],
    "update_time": "2018-08-01T21:52:13.962Z",
    "create_time": "2018-08-01T21:52:13.962Z",
    "invoice_number": "INPA-1533160333962",
    "state": "created",
    "intent": "sale",
    "id": "5b622b8ddd053a001662dd5a"
}
´´´
Posibles estados de la transacción:
  
| State    | Definición                               |
| -------- | ---------------------------------------- |
| created | El cargo no se ha ejecutado |
| paid  | El cargo fue realizado exitosamente en la cuenta del cliente |
| rejected | El sistema rechazo el cargo |
