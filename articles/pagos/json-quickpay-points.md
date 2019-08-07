## Ejemplo petición payment_method": "CMR_POINTS"
Esta petición es para puntos mas pesos. Si se quiere realizar una consulta de solo puntos, se debe setear los campos transaction.amount.total = 0 y transaction.amount.details.subtotal = 0.

```
curl -X POST \
https://api.qa.peinau.fif.tech/checkout/payments \
  -H 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJwcmltYXJ5c2lkIjoiNWI0NTIzNWI5Yzk4ZmMwZmJkZmZhZGJkIiwidW5pcXVlX25hbWUiOiJDTVIgQ2hpbGUiLCJncm91cHNpZCI6IkFQUEwiLCJpc3MiOiJGYWxhYmVsbGEiLCJhdWQiOiJXZWIiLCJ0eXBlIjoiQmVhcmVyIiwic2NvcGUiOltdLCJpYXQiOjE1NTQyMzA2NDYsImV4cCI6MTU1NDMxNzA0Nn0.h-uywTzLX8V5mEF1V6jCTnW0wZK0FVXj4KCcD-8IyNHzGpRU48JVa0urJlcv9vDLlRzxBelw8HM5aOBX7byxWCs4wUuiCne6R1801CPWp1YbXhXy0JbFgOhYw2Jsf0ij0S0eXx7--6BYhTbUZWYDNRU6iUAGjF5EhqEAfT_Z5ROGGVZLygBf3C17Nkhlu0JherZtKJAI_7PUSqKeP2o2Dd4ULaXVBqGzP6Uz2aCFqfhFPaCutIg6uGqDFdEGmNp5hHJAaAQ-uie8oqwwOWG0ZGJhkAT5kU5FXsOmRLXQkjq41cv-3xMY_oGQfZUT6fBx5MrrKPUGolRevBKjm1hWPQ' \
  -H 'Cache-Control: no-cache' \
  -H 'Content-Type: application/json' \
  -H 'Postman-Token: cdac848b-47c9-4e5e-bdfb-b20ccb675f9a' \
  -d '{
"intent": "sale",
"payer": {
  "payer_info": {
    "is_guest": "true",
    "email": "jhondoe@gmail.com",
    "full_name": "Jhon Doñe",
    "country": "CL",
    "document_number": "177694886",
    "document_type": "RUT"
  },
  "payment_method": "CMR_POINTS"
},
"transaction": {
  "description": "Transaction detailed description",
  "soft_descriptor": "Transaction Short description",
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
  "points_amount": {
    "currency": "CMR",
    "total": 10
  },
  "item_list": {
    "shipping_address": {
      "line1": "General Carol Urzua 1020, Depto 102A",
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
        "quantity": 1,
        "price": 500,
        "tax": 0,
        "category": "Vuelos"
      }
    ]
  }
},
"purchase_order": {
  "purchase_order_id": "536155295217"
},
"redirect_urls": {
  "return_url": "http://portal.sandbox.connect.fif.tech",
  "cancel_url": "http://portal.sandbox.connect.fif.tech"
},
"additional_attributes": {
  "query_id": "ID_INTENCION_DE_CONSULTA",
  "point_type": "CMR_PUNTOS",
  "installments_offer": [
	  "1",
	  "3",
	  "6"
	],
	"default_installment_number": "3",
	"default_deferred_month": "3"
}
}'
 
```

**Importante**, cabe mencionar que el atributo **payer.payer_info.is_guest** se rige bajo el siguiente criterio:

| **is_guest**        | **document_number**             | **query_id**  | **Tiempo desde la consulta** | **Acción**            |
| ------------------- | ------------------------------- | ------------- | ---------------------------- | --------------------- |
| "true"              | Viene (opcional)	        | No viene      | N/A                          | Se pide multiclave y se muestra rut por defecto, se permite cambio de rut |
| "true"              | Viene (opcional)	        | Viene         | < 3 minutos		       | Se omite autenticación de 1er factor    |
| "true"              | Viene (opcional)	        | Viene		| > 3 minutos		       | Se pide multiclave y se muestra rut por defecto, se permite cambio de rut |
| "true"              | No viene (opcional)		| Viene         | < 3 minutos		       | Se omite autenticación de 1er factor (QP obtiene RUT de intención de consulta) |
| "true" 	      | No viene (opcional)     	| Viene		| > 3 minutos		       | Se pide multiclave y rut |
| "true"              | No viene (opcional) 	        | No viene 	| N/A 			       | Se pide multiclave y rut |
| "false" 	      | Viene (obligatorio)		| No viene	| N/A			       | Se omite autenticación de 1er factor |
| "false"	      | Viene (obligatorio)		| Viene		| < 3 minutos		       | Se omite autenticación de 1er factor |
| "false"	      | Viene (obligatorio)		| Viene		| > 3 minutos		       | Se omite autenticación de 1er factor |
| "false"	      | No viene (obligatorio)		| Viene		| < 3 minutos		       | Devolvemos un error |
| "false"	      | No viene (obligatorio)		| Viene		| > 3 minutos		       | Devolvemos un error |
| "false"	      | No viene (obligatorio)		| No viene	| N/A			       | Devolvemos un error |


A continuación se presenta ejemplo de un JSON de respuesta obtenido al crear una intención de pago a través de la API RESTful de checkout:

```
{
  "application": "5b76f2ef3eb77128dda44168",
  "_id": "5ca4e4894fec1e0016a6d72b",
  "purchase_order": {
    "purchase_order_id": "536155295217"
  },
  "additional_attributes": {
    "point_type": "CMR_PUNTOS",
    "installments_offer": [
      "1",
      "3",
      "6"
    ],
    "default_installment_number": "3",
    "default_deferred_month": "3"
  },
  "redirect_urls": {
    "return_url": "http://portal.sandbox.connect.fif.tech",
    "cancel_url": "http://portal.sandbox.connect.fif.tech"
  },
  "transaction": {
    "gateway_order": "IP-15543102814894321",
    "description": "Transaction detailed description",
    "soft_descriptor": "Transaction Short description",
    "amount": {
      "details": {
        "shipping_discount": 0,
        "shipping": 0,
        "tax": 0,
        "subtotal": 100
      },
      "total": 100,
      "currency": "CLP"
    },
    "item_list": {
      "shipping_method": "DIGITAL",
      "items": [
        {
          "thumbnail": "http://portal.sandbox.connect.fif.tech/bundles/app/css/images/e-commerce-demo/product-icon.png",
          "sku": "TRK345-2",
          "name": "Flight 2344",
          "description": "Flight SCL - ONT",
          "quantity": 1,
          "price": 500,
          "tax": 0,
          "category": "Vuelos"
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
    "points_amount": {
      "currency": "CMR",
      "total": 10
    }
  },
  "payer": {
    "payer_info": {
      "is_guest": "true",
      "document_type": "RUT",
      "document_number": "177694886",
      "country": "CL",
      "full_name": "Jhon Doñe",
      "email": "jhondoe@gmail.com"
    },
    "payment_method": "CMR_POINTS"
  },
  "links": [
    {
      "href": "https://api.qa.peinau.fif.tech/checkout/payments/5ca4e4894fec1e0016a6d72b",
      "rel": "self",
      "method": "GET"
    },
    {
      "href": "https://api.qa.peinau.fif.tech/checkout/payments/gateways/cmr/points/5ca4e4894fec1e0016a6d72b/pay",
      "rel": "approval_url",
      "method": "REDIRECT"
    },
    {
      "href": "https://api.qa.peinau.fif.tech/checkout/payments/5ca4e4894fec1e0016a6d72b/edit",
      "rel": "update_url",
      "method": "PUT"
    },
    {
      "href": "https://api.qa.peinau.fif.tech/checkout/payments/gateways/cmr/points/5ca4e4894fec1e0016a6d72b/void",
      "rel": "void_method",
      "method": "POST"
    },
    {
      "href": "https://api.qa.peinau.fif.tech/checkout/payments/gateways/cmr/points/5ca4e4894fec1e0016a6d72b/refund",
      "rel": "refund_method",
      "method": "POST"
    },
    {
      "href": "https://api.qa.peinau.fif.tech/checkout/payments/IP-15543102814894321",
      "rel": "self_by_gateway_order",
      "method": "GET"
    }
  ],
  "update_time": "2019-04-03T16:51:21.489Z",
  "create_time": "2019-04-03T16:51:21.489Z",
  "invoice_number": "IP-15543102814894321",
  "state": "created",
  "intent": "sale",
  "id": "5ca4e4894fec1e0016a6d72b"
}
```

## Obtendrás los Links en la respuesta:

self: desde esta URL puedes consultar la información del pago.

approval_url: debes desplegar esta URL al cliente para que pueda continuar con el pago.

refund_method: te permite anular la transacción.

void_method: te permite cancelar la transacción.

self_by_gateway_order: desde esta URL también puedes consultar la información del pago utilizando el gateway_order.

## Consultar la información de la transación:

Cuando se realiza una búsqueda para transacción se obtienen estos datos: 


```
{
     "_id": "5ca4ea4157a18100167f15de",
     "application": "5b76f2ef3eb77128dda44168",
     "purchase_order": {
       "purchase_order_id": "536155295217"
     },
     "additional_attributes": {
       "point_type": "CMR_PUNTOS",
       "installments_offer": [
        "1",
        "3",
        "6"
      ],
      "default_installment_number": "3",
      "default_deferred_month": "3"
     },
     "redirect_urls": {
       "return_url": "http://portal.sandbox.connect.fif.tech",
       "cancel_url": "http://portal.sandbox.connect.fif.tech"
     },
     "transaction": {
       "gateway_order": "IP-15543117451723941",
       "description": "Transaction detailed description",
       "soft_descriptor": "Transaction Short description",
       "item_list": {
         "items": [
           {
             "thumbnail": "http://portal.sandbox.connect.fif.tech/bundles/app/css/images/e-commerce-demo/product-icon.png",
             "sku": "TRK345-2",
             "name": "Product 1",
             "description": "Flight SCL - ONT",
             "quantity": 1,
             "price": 500,
             "tax": 0,
             "category": "Vuelos"
           }
         ]
       },
       "points_amount": {
         "currency": "LOY",
         "total": 100
       }
     },
     "payer": {
       "payer_info": {
         "is_guest": "true",
         "email": "jhondoe@gmail.com",
         "full_name": "Jhon Doñe",
         "country": "CL",
         "document_number": "371377387",
         "document_type": "RUT"
       },
       "payment_method": "CMR_POINTS"
     },
     "links": [
       {
         "href": "https://api.qa.peinau.fif.tech/checkout/payments/5ca4ea4157a18100167f15de",
         "rel": "self",
         "method": "GET"
       },
       {
         "href": "https://api.qa.peinau.fif.tech/checkout/payments/gateways/cmr/points/5ca4ea4157a18100167f15de/pay",
         "rel": "approval_url",
         "method": "REDIRECT"
       },
       {
         "href": "https://api.qa.peinau.fif.tech/checkout/payments/5ca4ea4157a18100167f15de/edit",
         "rel": "update_url",
         "method": "PUT"
       },
       {
         "href": "https://api.qa.peinau.fif.tech/checkout/payments/gateways/cmr/points/5ca4ea4157a18100167f15de/void",
         "rel": "void_method",
         "method": "POST"
       },
       {
         "href": "https://api.qa.peinau.fif.tech/checkout/payments/gateways/cmr/points/5ca4ea4157a18100167f15de/refund",
         "rel": "refund_method",
         "method": "POST"
       }
     ],
     "update_time": "2019-04-03T17:15:45.172Z",
     "create_time": "2019-04-03T17:15:45.172Z",
     "invoice_number": "IP-15543117451723941",
     "state": "created",
     "intent": "sale",
     "id": "5ca4ea4157a18100167f15de"
   }
```
## Mostrar Formulario Pago con puntos mas pesos

Con la **approval_url** de la respuesta de la intención de captura, puedes iniciar el flujo de pago de puntos/puntos mas pesos

![Ejemplo de Apertura de iframe de pago-con-puntos](images/apertura-iframe-1.png)

El cliente debe ingresar los datos de rut y multiclave, seleccionar las cuotas, pasar la prueba de segundo factor y aprobar el pago para que nuestro sistema pueda ejecutar el cargo a la tarjeta de crédito. 

## Reversar una compra.

Para reversar una compra, se debe usar el método **void**. No se envía nada en el cuerpo del request. Al reversar obtendremos un json de respuesta exitosa con el estado de la transacción en estado **voided**. A continuación un ejemplo:
```
{
    "_id": "5d07e6ed14c196001682b171",
    "application": "5ae7359a6a3635000fafbc4c",
    "gateway": {
        "void": [
            {
                "merchTxnId": "IP-15607989574491991-CMR",
                "code": "SUCCESSFUL_REVERSAL",
                "message": "successful reversal",
                "statusCode": 200
            },
            {
                "merchTxnId": "IP-15607989574491991",
                "code": "SUCCESSFUL_REVERSAL",
                "message": "successful reversal",
                "statusCode": 200
            }
        ],
        "postMessage": {
            "msgType": "PayWithPointsResponse",
            "responseCode": 0,
            "responseDescription": "Success",
            "UUID": "3d0c790d-8e78-4021-a128-4c6b2b410e0e",
            "transactionId": "3d0c790d-8e78-4021-a128-4c6b2b410e0e"
        },
        "status": {
            "uuid": "3d0c790d-8e78-4021-a128-4c6b2b410e0e",
            "status": "DONE_POINTS",
            "errorDescription": "",
            "paymentTransactionDetails": [
                {
                    "status": "success",
                    "authorizationCode": "168817670954",
                    "type": "CreditPayment",
                    "qpTxnId": 3519693,
                    "amount": 100,
                    "accountFirst6": "111120",
                    "accountLast4": "9968"
                },
                {
                    "status": "success",
                    "authorizationCode": "168817670955",
                    "type": "PointsPayment",
                    "qpTxnId": 3519694,
                    "amount": 5000
                }
            ],
            "createdDate": "2019-06-17T19:16:13.330Z",
            "updatedDate": "2019-06-17T19:17:35.758Z",
            "logTrackId": "#LGID=f674ad23702742409632b0cc23bb0ec3#MID=007407719#CHID=WEB#PYMT=P#DT=RUT#DID=159299740#UUID=3d0c790d-8e78-4021-a128-4c6b2b410e0e#TID=IP-15607989574491991#"
        },
        "resume": {
            "response": {
                "code": 0
            },
            "transaction": {
                "installments_number": 1,
                "points_amount": 5000,
                "amount": 0,
                "buy_order": "IP-15607989574491991",
                "currency": "LOY",
                "date": "2019-06-17T19:17:37.423Z",
                "type": "CREDIT",
                "gateway_id": "3d0c790d-8e78-4021-a128-4c6b2b410e0e"
            },
            "authorizations": {
                "code": "168817670954"
            },
            "_id": "5d07e751e30f18001643edb0"
        }
    },
    "purchase_order": {
        "purchase_order_id": "00536155295217"
    },
    "additional_attributes": {
        "point_type": "CMR_PUNTOS",
        "installments_offer": [
            "1",
            "3",
            "6"
        ],
        "default_installment_number": "3",
        "default_deferred_month": "3"
    },
    "redirect_urls": {
        "return_url": "https://www.falabella.com",
        "cancel_url": "https://www.google.com"
    },
    "transaction": {
        "gateway_order": "IP-15607989574491991",
        "reference_id": "OD0000233",
        "description": "Transaction detailed description",
        "soft_descriptor": "Transaction Short description",
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
            "shipping_method": "DIGITAL",
            "items": [
                {
                    "thumbnail": "http://portal.sandbox.connect.fif.tech/bundles/app/css/images/e-commerce-demo/product-icon.png",
                    "sku": "000000000009735780",
                    "category": "Electronica",
                    "name": "Tostador",
                    "description": "Tostador",
                    "quantity": 1,
                    "price": 100,
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
        "points_amount": {
            "currency": "CMR",
            "total": 5000
        }
    },
    "payer": {
        "payer_info": {
            "email": "jhondoe@gmail.com",
            "full_name": "Jhon Doe",
            "country": "CL",
            "document_number": "159299740",
            "document_type": "RUT",
            "is_guest": "true"
        },
        "payment_method": "CMR_POINTS"
    },
    "links": [
        {
            "href": "https://api.qa.peinau.fif.tech/checkout/payments/5d07e6ed14c196001682b171",
            "rel": "self",
            "method": "GET"
        },
        {
            "href": "https://api.qa.peinau.fif.tech/checkout/payments/gateways/cmr/points/5d07e6ed14c196001682b171/pay",
            "rel": "approval_url",
            "method": "REDIRECT"
        },
        {
            "href": "https://api.qa.peinau.fif.tech/checkout/payments/5d07e6ed14c196001682b171/edit",
            "rel": "update_url",
            "method": "PUT"
        },
        {
            "href": "https://api.qa.peinau.fif.tech/checkout/payments/gateways/cmr/points/5d07e6ed14c196001682b171/void",
            "rel": "void_method",
            "method": "POST"
        },
        {
            "href": "https://api.qa.peinau.fif.tech/checkout/payments/gateways/cmr/points/5d07e6ed14c196001682b171/refund",
            "rel": "refund_method",
            "method": "POST"
        }
    ],
    "update_time": "2019-06-17T19:18:04.212Z",
    "create_time": "2019-06-17T19:15:57.449Z",
    "invoice_number": "IP-15607989574491991",
    "state": "voided",
    "intent": "sale",
    "id": "5d07e6ed14c196001682b171"
}
```

## Anular una compra.
Para anular una compra, se debe usar el método **refund** con el siguiente body request con los valores respectivos a anular en puntos y en pesos. 

```
{
    "refunded_points_amount": 5000,
    "refunded_amount": 100
}
```

Al anular obtendremos un json de respuesta exitosa con el estado de la transacción en estado **partially_refunded** si la anulación no contempló anular todos los puntos y pesos; y en **refunded** si la anulación contempló la totalidad de los puntos y los pesos. A continuación un ejemplo:

```
{
    "_id": "5d07ec36ea04da644b15cf67",
    "application": "5ae7359a6a3635000fafbc4c",
    "gateway": {
        "refunds": [
            {
                "items": [
                    {
                        "description": "Tostador",
                        "totalPrice": 100,
                        "quantity": 1,
                        "pricePerUnit": 100,
                        "category": "Electronica",
                        "sku": "000000000009735780"
                    }
                ],
                "refunded_amount": 100,
                "message": "successful refund",
                "refundResponseCode": 0,
                "refundResponseDescription": "Success",
                "refundCancellationCode": "168817670965",
                "refundTxnId": "3519704",
                "type": "CreditPayment"
            },
            {
                "items": [
                    {
                        "description": "Tostador",
                        "totalPrice": 100,
                        "quantity": 1,
                        "pricePerUnit": 100,
                        "category": "Electronica",
                        "sku": "000000000009735780"
                    }
                ],
                "refunded_amount": 5000,
                "message": "successful refund",
                "refundResponseCode": 0,
                "refundResponseDescription": "Success",
		"refundCancellationCode": "168817670966",
                "refundTxnId": "3519705",
                "type": "PointsPayment"
            }
        ],
        "postMessage": {
            "msgType": "PayWithPointsResponse",
            "responseCode": 0,
            "responseDescription": "Success",
            "UUID": "6448bc2e-bb90-413f-b945-e0a672ac6e85",
            "transactionId": "6448bc2e-bb90-413f-b945-e0a672ac6e85"
        },
        "status": {
            "uuid": "6448bc2e-bb90-413f-b945-e0a672ac6e85",
            "status": "DONE_POINTS",
            "errorDescription": "",
            "paymentTransactionDetails": [
                {
                    "status": "success",
                    "authorizationCode": "168817670963",
                    "type": "CreditPayment",
                    "qpTxnId": 3519702,
                    "amount": 100,
                    "accountFirst6": "111149",
                    "accountLast4": "6809"
                },
                {
                    "status": "success",
                    "authorizationCode": "168817670964",
                    "type": "PointsPayment",
                    "qpTxnId": 3519703,
                    "amount": 5000
                }
            ],
            "createdDate": "2019-06-17T19:37:23.461Z",
            "updatedDate": "2019-06-17T19:38:28.882Z",
            "logTrackId": "#LGID=28c4e5a96bb0531b2a53e4343b60cf60#MID=007407719#CHID=WEB#PYMT=P#DT=RUT#DID=159299740#UUID=6448bc2e-bb90-413f-b945-e0a672ac6e85#TID=IP-15608003100143211#"
        },
        "resume": {
            "response": {
                "code": 0
            },
            "transaction": {
                "installments_number": 1,
                "points_amount": 5000,
                "amount": 0,
                "buy_order": "IP-15608003100143211",
                "currency": "LOY",
                "date": "2019-06-17T19:39:46.698Z",
                "type": "CREDIT",
                "gateway_id": "6448bc2e-bb90-413f-b945-e0a672ac6e85"
            },
            "authorizations": {
                "code": "168817670963"
            },
            "_id": "5d07ec82ea04da644b15cf69"
        }
    },
    "purchase_order": {
        "purchase_order_id": "00536155295217"
    },
    "additional_attributes": {
        "point_type": "CMR_PUNTOS",
        "installments_offer": [
            "1",
            "3",
            "6"
        ],
        "default_installment_number": "3",
        "default_deferred_month": "3"
    },
    "redirect_urls": {
        "return_url": "https://www.falabella.com",
        "cancel_url": "https://www.google.com"
    },
    "transaction": {
        "gateway_order": "IP-15608003100143211",
        "reference_id": "OD0000233",
        "description": "Transaction detailed description",
        "soft_descriptor": "Transaction Short description",
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
            "shipping_method": "DIGITAL",
            "items": [
                {
                    "thumbnail": "http://portal.sandbox.connect.fif.tech/bundles/app/css/images/e-commerce-demo/product-icon.png",
                    "sku": "000000000009735780",
                    "category": "Electronica",
                    "name": "Tostador",
                    "description": "Tostador",
                    "quantity": 1,
                    "price": 100,
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
        "points_amount": {
            "currency": "CMR",
            "total": 5000
        }
    },
    "payer": {
        "payer_info": {
            "email": "jhondoe@gmail.com",
            "full_name": "Jhon Doe",
            "country": "CL",
            "document_number": "159299740",
            "document_type": "RUT",
            "is_guest": "true"
        },
        "payment_method": "CMR_POINTS"
    },
    "links": [
        {
            "href": "http://localhost:8081/payments/5d07ec36ea04da644b15cf67",
            "rel": "self",
            "method": "GET"
        },
        {
            "href": "http://localhost:8081/payments/gateways/cmr/points/5d07ec36ea04da644b15cf67/pay",
            "rel": "approval_url",
            "method": "REDIRECT"
        },
        {
            "href": "http://localhost:8081/payments/5d07ec36ea04da644b15cf67/edit",
            "rel": "update_url",
            "method": "PUT"
        },
        {
            "href": "http://localhost:8081/payments/gateways/cmr/points/5d07ec36ea04da644b15cf67/void",
            "rel": "void_method",
            "method": "POST"
        },
        {
            "href": "http://localhost:8081/payments/gateways/cmr/points/5d07ec36ea04da644b15cf67/refund",
            "rel": "refund_method",
            "method": "POST"
        }
    ],
    "update_time": "2019-06-17T19:40:09.125Z",
    "create_time": "2019-06-17T19:38:30.014Z",
    "invoice_number": "IP-15608003100143211",
    "state": "refunded",
    "intent": "sale",
    "id": "5d07ec36ea04da644b15cf67"
}
```

Un ejemplo de error en el proceso de anulación:
```
{
    "error_code": "INVALID_HTTP_STATUS_CODE_IN_REQUEST",
    "error_description": "The request return a invalid status code response",
    "meta_data": {
        "errors": [
            {
                "message": "An error has occurred while refunding transaction.",
                "code": "REFUND_ERROR"
            }
        ]
    }
}
```
