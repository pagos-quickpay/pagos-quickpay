## Crear Intención de pago

Para contiunar con el proceso de pago, debes ingresar en el header de la petición el [access_token](obtener-token-acceso.md) generado en el paso anterior y hacer el llamado de la siguiente forma:

```
curl -X POST 'https://api.sandbox.connect.fif.tech/checkout/payments' \
 -H "Content-Type: application/json" \
 -H "Authorization: Bearer REEMPLAZAR AQUI EL ACCESS TOKEN" \
 -d '{ 
{ 
   "intent": "sale", 
   "payer": { 
     "payer_info": { 
       "email": "jlprueba1@quickpay.com", 
       "full_name": "Andres Roa",
       "country": "CL",
       "document_number": "123123123",
       "document_type": "RUT"
     }, 
     "payment_method": "TRANSBANK_WEBPAY"
   }, 
   "transaction": { 
     "reference_id": "OD0000233", 
     "gateway_order": "QP00009",
     "description": "Transaction detailed description", 
     "soft_descriptor": "Short Description", 
     "amount": { 
       "currency": "CLP", 
       "total": 4500, 
       "details": { 
         "subtotal": 810, 
         "tax": 190, 
         "shipping": 0, 
         "shipping_discount": 0 
       } 
     }, 
     "item_list": { 
       "shipping_address": { 
         "line1": "Miraflores 222", 
         "city": "Santiago", 
         "country_code": "CL", 
         "phone": "+56 9 1234 5674", 
         "type": "HOME_OR_WORK", 
         "recipient_name": "Andres Roa" 
       }, 
       "shipping_method": "DIGITAL", 
       "items": [ 
         { 
           "sku": "1231232", 
           "name": "Destornillador 2344", 
           "description": "Destornillador SCL - ONT", 
           "quantity": 1, 
           "price": 4500, 
           "tax": 0 
         } 
       ] 
     } 
   }, 
   "redirect_urls": { 
     "return_url": "https://peinau.azureedge.net/redirections/payment_success.html", 
     "cancel_url": "https://chao.com" 
   },
   "additional_attributes": {
  }
 }' | json_pp
```

Como respuesta obtendrás la siguiente información:

```
{
    "application": "5af350553dbed900146c5945",
    "_id": "5c2ccf090105ab1daf59f855",
    "redirect_urls": {
        "return_url": "https://peinau.azureedge.net/redirections/payment_success.html",
        "cancel_url": "https://chao.com"
    },
    "transaction": {
        "reference_id": "OD0000233",
        "gateway_order": "QP00009",
        "description": "Transaction detailed description",
        "soft_descriptor": "Short Description",
        "item_list": {
            "shipping_method": "DIGITAL",
            "items": [
                {
                    "sku": "1231232",
                    "name": "Destornillador 2344",
                    "description": "Destornillador SCL - ONT",
                    "quantity": 1,
                    "price": 4500,
                    "tax": 0
                }
            ],
            "shipping_address": {
                "line1": "Miraflores 222",
                "city": "Santiago",
                "country_code": "CL",
                "phone": "+56 9 1234 5674",
                "type": "HOME_OR_WORK",
                "recipient_name": "Andres Roa"
            }
        },
        "amount": {
            "currency": "CLP",
            "total": 4500,
            "details": {
                "subtotal": 810,
                "tax": 190,
                "shipping": 0,
                "shipping_discount": 0
            }
        }
    },
    "payer": {
        "payer_info": {
            "document_type": "RUT",
            "document_number": "123123123",
            "country": "CL",
            "full_name": "Andres Roa",
            "email": "jlprueba1@quickpay.com"
        },
        "payment_method": "TRANSBANK_WEBPAY"
    },
    "links": [
        {
            "href": "https://api.sandbox.connect.fif.tech/checkout/payments/5c2ccf090105ab1daf59f855",
            "rel": "self",
            "method": "GET"
        },
        {
            "href": "https://api.sandbox.connect.fif.tech/checkout/payments/gateways/transbank/webpay/5c2ccf090105ab1daf59f855/pay",
            "rel": "approval_url",
            "method": "REDIRECT"
        },
        {
            "href": "https://api.sandbox.connect.fif.tech/checkout/payments/5c2ccf090105ab1daf59f855/edit",
            "rel": "update_url",
            "method": "PUT"
        },
        {
            "href": "https://api.sandbox.connect.fif.tech/checkout/payments/gateways/transbank/webpay/5c2ccf090105ab1daf59f855/acknowledge",
            "rel": "acknowledge_method",
            "method": "POST"
        },
        {
            "href": "https://api.sandbox.connect.fif.tech/checkout/payments/QP00009",
            "rel": "self_by_gateway_order",
            "method": "GET"
        }
    ],
    "update_time": "2019-01-02T14:47:37.595Z",
    "create_time": "2019-01-02T14:47:37.595Z",
    "invoice_number": "IP-15464404575959741",
    "state": "created",
    "intent": "sale",
    "id": "5c2ccf090105ab1daf59f855"
}
```

Obtendrás los Links:

- **self**: desde esta URL puedes consultar la información del pago.
- **approval_url**: debes desplegar esta URL al cliente para que pueda continuar con el pago.
- **acknowledge**: (FLUJO DEPRECADO) desde esta URL se realiza acknowledge a Transbank.
# Mostrar Formulario Checkout

Con la **approval_url** obtenida en el paso anterior debes desplegar el formulario de Checkout (pago). 
NOTA: En el flujo sin llamado del comercio al ACKNOWLEDGE el pago termina en estado 'paid', y no se deben realizar pasos extras para terminar la transacción. En caso de que su comercio aún utilize el flujo con ACKNOWLEDGE el pago termina en estado 'created' y se debe confirmar el pago en TRANSBANK a través del ACKNOWLEDGE para culminar el pago (pasar a paid).

## Consultar Estado de la Transacción

para consultar el estado (state) de la transacción necesitas enviar el **access_token** (en el header de la petición) obtenido en la **Autenticación**, la **url self** obtenida como respuesta de la intención de pago y ejecutar la consulta de la siguiente forma:

```
curl -X GET \
  https://api.sandbox.connect.fif.tech/checkout/payments/19a516df-b027-443e-be15-e44a41dbd94f \
  -H 'cache-control: no-cache' \
  -H 'Authorization: Bearer REEMPLAZAR AQUI EL ACCESS TOKEN'
```
Obtendrás una respuesta similar a:

  ```
{
    "_id": "5c2ccf090105ab1daf59f855",
    "application": "5af350553dbed900146c5945",
    "redirect_urls": {
        "return_url": "https://peinau.azureedge.net/redirections/payment_success.html",
        "cancel_url": "https://chao.com"
    },
    "transaction": {
        "reference_id": "OD0000233",
        "gateway_order": "QP00009",
        "description": "Transaction detailed description",
        "soft_descriptor": "Short Description",
        "item_list": {
            "shipping_method": "DIGITAL",
            "items": [
                {
                    "sku": "1231232",
                    "name": "Destornillador 2344",
                    "description": "Destornillador SCL - ONT",
                    "quantity": 1,
                    "price": 4500,
                    "tax": 0
                }
            ],
            "shipping_address": {
                "line1": "Miraflores 222",
                "city": "Santiago",
                "country_code": "CL",
                "phone": "+56 9 1234 5674",
                "type": "HOME_OR_WORK",
                "recipient_name": "Andres Roa"
            }
        },
        "amount": {
            "currency": "CLP",
            "total": 4500,
            "details": {
                "subtotal": 810,
                "tax": 190,
                "shipping": 0,
                "shipping_discount": 0
            }
        }
    },
    "payer": {
        "payer_info": {
            "email": "jlprueba1@quickpay.com",
            "full_name": "Andres Roa",
            "country": "CL",
            "document_number": "123123123",
            "document_type": "RUT"
        },
        "payment_method": "TRANSBANK_WEBPAY"
    },
    "links": [
        {
            "href": "https://api.sandbox.connect.fif.tech/checkout/payments/5c2ccf090105ab1daf59f855",
            "rel": "self",
            "method": "GET"
        },
        {
            "href": "https://api.sandbox.connect.fif.tech/checkout/payments/gateways/transbank/webpay/5c2ccf090105ab1daf59f855/pay",
            "rel": "approval_url",
            "method": "REDIRECT"
        },
        {
            "href": "https://api.sandbox.connect.fif.tech/checkout/payments/5c2ccf090105ab1daf59f855/edit",
            "rel": "update_url",
            "method": "PUT"
        },
        {
            "href": "https://api.sandbox.connect.fif.tech/checkout/payments/gateways/transbank/webpay/5c2ccf090105ab1daf59f855/acknowledge",
            "rel": "acknowledge_method",
            "method": "POST"
        }
    ],
    "update_time": "2019-01-02T14:47:37.595Z",
    "create_time": "2019-01-02T14:47:37.595Z",
    "invoice_number": "IP-15464404575959741",
    "state": "created",
    "intent": "sale",
    "id": "5c2ccf090105ab1daf59f855"
}
```
Posibles estados de la transacción hasta este punto:
  
| State    | Definición                               |
| -------- | ---------------------------------------- |
| paid  | El cargo fue realizado exitosamente en la cuenta del cliente |
| rejected | El cargo no fue realizado |


## Acknowledge (FLUJO DEPRECADO)
Para confirmar una transacción en TRANSBANK una vez concluido el pago se debe llamar a esta URL en menos de 25 segundos una vez concluido el pago, de no llamar en este rango de tiempo la transacción no será confirmada por Transbank y se rechazará el pago. Ejemplo llamado:


```
curl -X POST \
  https://api.sandbox.connect.fif.tech/checkout/payments/gateways/transbank/webpay/5c2ccf090105ab1daf59f855/acknowledge \
  -H 'cache-control: no-cache' \
  -H 'Authorization: Bearer REEMPLAZAR AQUI EL ACCESS TOKEN'
```

Obtendrás una respuesta similar a:

  ```
{
    "_id": "5c2cc7630105ab1daf59f84d",
    "application": "5af350553dbed900146c5945",
    "gateway": {
        "resume": {
            "_id": "5c2cc7940105ab1daf59f84e",
            "card_number": {
                "pan_last4": "1111"
            },
            "authorizations": {
                "code": "706202"
            },
            "transaction": {
                "gateway_id": "5c2cc7630105ab1daf59f84d",
                "type": "DEBIT",
                "date": "2019-01-02T14:15:48.452Z",
                "currency": "CLP",
                "buy_order": "prueba_tbk_1",
                "amount": 1000,
                "installments_number": 0
            },
            "response": {
                "code": 0
            }
        },
        "accountingDate": "0102",
        "buyOrder": "prueba_tbk_1",
        "cardDetail": {
            "cardNumber": "1111"
        },
        "detailOutput": [
            {
                "sharesNumber": 0,
                "amount": "1000",
                "commerceCode": "597020000541",
                "buyOrder": "prueba_tbk_1",
                "authorizationCode": "706202",
                "paymentTypeCode": "VD",
                "responseCode": 0
            }
        ],
        "sessionId": "5c2cc7630105ab1daf59f84d",
        "transactionDate": "2019-01-02T14:15:15.261Z",
        "urlRedirection": "https://webpay3gint.transbank.cl/webpayserver/voucher.cgi",
        "VCI": "TSY",
        "transaction_token": "ee8ca655dc9e1376c7c397d3c2c4ee9f0d89118e8c1dc4e95a88d4cc047724d6",
        "operationDates": {
            "ackDate": "2019-01-02T14:15:47.961Z",
            "commerceACK": "2019-01-02T14:15:47.842Z",
            "tbkNotifiyDate": "2019-01-02T14:15:37.659Z",
            "fetchResultDate": "2019-01-02T14:15:38.444Z"
        }
    },
    "redirect_urls": {
        "return_url": "https://www.falabella.com",
        "cancel_url": "https://www.google.com"
    },
    "transaction": {
        "gateway_order": "prueba_tbk_1",
        "description": "Transaction detailed description",
        "soft_descriptor": "Transaction Short description",
        "item_list": {
            "shipping_method": "DIGITAL",
            "items": [
                {
                    "thumbnail": "http://localhost:8000/bundles/app/css/images/e-commerce-demo/product-icon.png",
                    "sku": "TRK345-2",
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
            "document_number": "107872388",
            "document_type": "RUT"
        },
        "payment_method": "TRANSBANK_WEBPAY"
    },
    "links": [
        {
            "href": "https://api.sandbox.connect.fif.tech/checkout/payments/5c2cc7630105ab1daf59f84d",
            "rel": "self",
            "method": "GET"
        },
        {
            "href": "https://api.sandbox.connect.fif.tech/checkout/payments/gateways/transbank/webpay/5c2cc7630105ab1daf59f84d/pay",
            "rel": "approval_url",
            "method": "REDIRECT"
        },
        {
            "href": "https://api.sandbox.connect.fif.tech/checkout/payments/5c2cc7630105ab1daf59f84d/edit",
            "rel": "update_url",
            "method": "PUT"
        },
        {
            "href": "https://api.sandbox.connect.fif.tech/checkout/payments/gateways/transbank/webpay/5c2cc7630105ab1daf59f84d/acknowledge",
            "rel": "acknowledge_method",
            "method": "POST"
        }
    ],
    "update_time": "2019-01-02T14:15:48.454Z",
    "create_time": "2019-01-02T14:14:59.592Z",
    "invoice_number": "IP-15464384995920801",
    "state": "paid",
    "intent": "sale",
    "id": "5c2cc7630105ab1daf59f84d"
}
```

El objeto operationDates guarda la hora en que Transbank avisa la culminación del pago, y cuando se ejecutan los acknowledge del comercio a Connect y Connect a Transbank.

```
    "operationDates": {
          "ackDate": "2019-01-02T14:15:47.961Z", (Hora se envía ACK a Transbank)
          "commerceACK": "2019-01-02T14:15:47.842Z", (Hora Comercio envía ACK a Connect)
          "tbkNotifiyDate": "2019-01-02T14:15:37.659Z", (Hora Transbank avisa a Connect cliente termina Pago)
          "fetchResultDate": "2019-01-02T14:15:38.444Z" (Hora Connect consulta estado transacción en Transbank, inmediatamente después se enva notificación al Comercio de la culminación del pago)
      }
```
