# Ejemplo de silent charge fallido


## Rechazado por el Gateway (HTTP 200)

Necesitas el **access_token** obtenido en la **Autenticación** y la **url silent charge** obtenida en el [paso 4](intencion-de-pago.md) para ejecutar una llamada a la **API de Silent Charge /silent** de la siguiente forma:

```
 curl -v -X POST 'https://api.sandbox.connect.fif.tech/checkout/payments/gateways/quickpay/token/25c30852-33ae-927a-02c9-80bc6c9afb74/silent' \
 -H "Content-Type: application/json" \
 -H "Authorization: Bearer access_token"
 -d '{
	"installments_number": 36
}'
```
Obtendras una respuesta similar a:

```
{  
   "intent":"sale",
   "additional_attributes":{  
      "capture_token":"c923e853-a8ce-7a53-508d-4974ffe90aca",
      "remember_capture":false
   },
   "application":"195d24b8-ff4b-1803-a405-cbcd5e8a8b7d",
   "redirect_urls":{  
      "return_url":"https://requestb.in/sfoogtsf",
      "cancel_url":"https://chao.com"
   },
   "transaction":{  
      "reference_id":"OD0000233",
      "description":"Transaction detailed description",
      "soft_descriptor":"Short Description",
      "item_list":{  
         "shipping_method":"DIGITAL",
         "items":[  
            {  
               "sku":"1231232",
               "name":"Destornillador 2344",
               "description":"Destornillador SCL - ONT",
               "quantity":1,
               "price":4500,
               "tax":0,
               "_id":"5a71e36e0f94ef000f1ce8fd"
            }
         ],
         "shipping_address":{  
            "line1":"Miraflores 222",
            "city":"Santiago",
            "country_code":"CL",
            "phone":"+56 9 1234 5674",
            "type":"HOME_OR_WORK",
            "recipient_name":"Andres Roa"
         }
      },
      "amount":{  
         "currency":"CLP",
         "total":4500,
         "details":{  
            "subtotal":810,
            "tax":190,
            "shipping":0,
            "shipping_discount":0
         }
      },
      "gateway_order":"INPA-0000004017"
   },
   "payer":{  
      "payer_info":{  
         "documentType":"RUT",
         "documentNumber":"123123123",
         "country":"CL",
         "full_name":"Andres Roa",
         "email":"jlprueba2@quickpay.com"
      },
      "payment_method":"QUICKPAY_TOKEN"
   },
   "links":[  

   ],
   "id":"d33ee1f8-df10-edcc-9762-949aa2f5ed24",
   "create_time":"2018-01-31T15:40:30.416Z",
   "update_time":"2018-01-31T15:40:42.148Z",
   "state":"rejected",
   "invoice_number":"INPA-0000004017",
   "gateway":{  
      "error":{  
         "error_code":"GW01_481",
         "error_description":"The order has been rejected by Decision Manager.",
         "meta_data":{  
            "gateway_data":{  
               "merchantReferenceCode":"INPA-0000004017",
               "requestID":"5174132415356813504008",
               "decision":"REJECT",
               "reasonCode":"481",
               "requestToken":"Ahjz7wSTGH2DAgngxO4IigFLgFisvPJgbGUfX14dJMvRiuX5YATkxh9gwIJ4MTuCAAAAbQ1c",
               "afsReply":{  
                  "reasonCode":"100",
                  "afsResult":"41",
                  "binCountry":"US",
                  "cardAccountType":"Visa Gold",
                  "cardScheme":"VISA CREDIT",
                  "cardIssuer":"RIVER VALLEY CREDIT UNION",                  
               }
            },
            "decisionReply":{  
               "casePriority":"2",
               "activeProfileReply":""
            }
         }
      },
      "amount":4500,
      "capture_token":"c923e853-a8ce-7a53-508d-4974ffe90aca"
   }
}
```

Para este caso, cuando el resultado del silent es fallido, el campo state de la respuesta tendrá el valor **rejected** y será posible ver el detalle en **gateway.error**.

Al consultar el estado de la transacción (self):

```
curl -X GET \
  https://api.sandbox.connect.fif.tech/checkout/payments/{id} \
  -H 'authorization: access_token' \
 ```

Obtendrás una respuesta similar a:

```
{
    "intent": "sale",
    "additional_attributes": {
        "capture_token": "c923e853-a8ce-7a53-508d-4974ffe90aca",
        "remember_capture": false
    },
    "application": "195d24b8-ff4b-1803-a405-cbcd5e8a8b7d",
    "redirect_urls": {
        "return_url": "https://requestb.in/sfoogtsf",
        "cancel_url": "https://chao.com"
    },
    "transaction": {
        "reference_id": "OD0000233",
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
                    "tax": 0,
                    "_id": "5a71e36e0f94ef000f1ce8fd"
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
        },
        "gateway_order": "INPA-0000004017"
    },
    "payer": {
        "payer_info": {
            "documentType": "RUT",
            "documentNumber": "123123123",
            "country": "CL",
            "full_name": "Andres Roa",
            "email": "jlprueba2@quickpay.com"
        },
        "payment_method": "QUICKPAY_TOKEN"
    },
    "links": [],
    "id": "d33ee1f8-df10-edcc-9762-949aa2f5ed24",
    "create_time": "2018-01-31T15:40:30.416Z",
    "update_time": "2018-01-31T15:40:42.148Z",
    "state": "rejected",
    "invoice_number": "INPA-0000004017",
   "gateway":{  
      "error":{  
         "error_code":"GW01_481",
         "error_description":"The order has been rejected by Decision Manager.",
         "meta_data":{  
            "gateway_data":{  
               "merchantReferenceCode":"INPA-0000004017",
               "requestID":"5174132415356813504008",
               "decision":"REJECT",
               "reasonCode":"481",
               "requestToken":"Ahjz7wSTGH2DAgngxO4IigFLgFisvPJgbGUfX14dJMvRiuX5YATkxh9gwIJ4MTuCAAAAbQ1c",
               "afsReply":{  
                  "reasonCode":"100",
                  "afsResult":"41",
                  "binCountry":"US",
                  "cardAccountType":"Visa Gold",
                  "cardScheme":"VISA CREDIT",
                  "cardIssuer":"RIVER VALLEY CREDIT UNION",                  
               }
            },
            "decisionReply":{  
               "casePriority":"2",
               "activeProfileReply":""
            }
         }
      },
      "amount":4500,
      "capture_token": "c923e853-a8ce-7a53-508d-4974ffe90aca"
    }
}
```


### Formato de rechazo en la respuesta del Gateway
| HTTP code| Respuesta del servicio                               |
| -------- | ---------------------------------------- |
|200 | **error_code**: GW01_XX, **error_description**: DESCRIPCION RETORNADA POR EL GATEWAY|

> Para este caso se debe consultar la [Lista de códigos de respuesta CyberSource](../api-tokenizacion-pago/cybersource_reason_code.md). Donde XX del **error_code** será el reason code respectivo y en el **error_description** estará expresada la descripción de dicho reason code de acuerdo al Gateway.

## Otros rechazos (HTTP code mayores a 400)

Necesitas el **access_token** obtenido en la **Autenticación** y la **url silent charge** obtenida en el [paso 4](intencion-de-pago.md) para ejecutar una llamada a la **API de Silent Charge /silent** de la siguiente forma:

Enviando un valor incorrecto en el id del pago para generar el error:

```
 curl -v -X POST 'https://api.sandbox.connect.fif.tech/checkout/payments/gateways/quickpay/token/xxx-xxx-xxx-xxx/silent' \
 -H "Content-Type: application/json" \
 -H "Authorization: Bearer access_token"
 -d '{
	"installments_number": 36
}''
```

Obtendrás una respuesta similar a:

```
{
    "error_code": "DOCUMENT_NOT_FOUND",
    "error_description": "the document you requested is not found",
    "meta_data": {
        "id_not_found": "d33ee1f8-df10-edcc-9762-949aa2f5ed2",
        "collection_name": "dbs/app-checkout-quickpay/colls/payment_intentions"
    }
}
```

> El http code de esta respuesta es 404 not found

Al consultar el estado de la transacción (self):

```
curl -X GET \
  https://api.sandbox.connect.fif.tech/checkout/payments/{id} \
  -H 'authorization: access_token' \
 ```
 
 Obtenndrás una respuesta similar a:
 
 ```
 {
    "intent": "sale",
    "additional_attributes": {
        "capture_token": "c923e853-a8ce-7a53-508d-4974ffe90aca"
    },
    "application": "195d24b8-ff4b-1803-a405-cbcd5e8a8b7d",
    "redirect_urls": {
        "return_url": "https://requestb.in/sfoogtsf",
        "cancel_url": "https://chao.com"
    },
    "transaction": {
        "reference_id": "OD0000233",
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
                    "tax": 0,
                    "_id": "5a71f5a4c68669000f63df10"
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
        },
        "gateway_order": "INPA-0000004018"
    },
    "payer": {
        "payer_info": {
            "documentType": "RUT",
            "documentNumber": "123123123",
            "country": "CL",
            "full_name": "Andres Roa",
            "email": "jlprueba2@quickpay.com"
        },
        "payment_method": "QUICKPAY_TOKEN"
    },
    "links": [],
    "id": "0bb99861-b6ed-b7f5-72a8-7e992d0b3907",
    "create_time": "2018-01-31T16:58:12.242Z",
    "update_time": "2018-01-31T16:58:12.242Z",
    "state": "created",
    "invoice_number": "INPA-0000004018"
}
 ```
 
Para este caso podrás observar que el campo state de la respuesta (self) mantendrá el valor **created**, esto debido a que el silent charge fue interrumpido antes de actualizar el estado del pago.

[Listado de errores para Silent Charge](errores-silent.md)
