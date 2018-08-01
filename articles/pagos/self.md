# ¿Cómo puedes consultar el estado de la transacción?

Debes llamar al self obtenido en la respuesta de la intención de pago de la siguiente forma:

```
curl -X GET \
  https://api.test.peinau.fif.tech/checkout/payments/{id} \
  -H 'authorization: access_token' \
 ```

Obtendrás una respuesta similar a:

```
{
    "_id": "5b622b8ddd053a001662dd5a",
    "application": "5ae7359a6a3635000fafbc4c",
    "additional_attributes": {
        "card_bin": 548740,
        "last_four_digits": "3038"
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
            "email": "jhondoe@gmail.com",
            "full_name": "Jhon Doe",
            "country": "CL",
            "document_number": "371377387",
            "document_type": "RUT"
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
        }
    ],
    "update_time": "2018-08-01T21:52:13.962Z",
    "create_time": "2018-08-01T21:52:13.962Z",
    "invoice_number": "INPA-1533160333962",
    "state": "created",
    "intent": "sale",
    "id": "5b622b8ddd053a001662dd5a"
}
```
> Esta información es identica a la respuesta obtenida en la respuesta de la intencion de pago

# Ejemplo de Self incorrecto

Enviando un id incorrecto

```
curl -X GET \
  https://api.test.peinau.fif.tech/checkout/payments/{id_incorrecto} \
  -H 'authorization: access_token' \
 ```

La respuesta obtenida es: 
* Status http **500**
* Glosa: **"DOCUMENT_NOT_FOUND"**
