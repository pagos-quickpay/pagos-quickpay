## Ejemplo petición payment_method": "CMR_POINTS"

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
  "point_type": "CMR_PUNTOS"
}
}'
 
```
 
A continuación se presenta ejemplo de un JSON de respuesta obtenido al crear una intención de pago a través de la API RESTful de checkout:

```
{
  "application": "5b76f2ef3eb77128dda44168",
  "_id": "5ca4e4894fec1e0016a6d72b",
  "purchase_order": {
    "purchase_order_id": "536155295217"
  },
  "additional_attributes": {
    "point_type": "CMR_PUNTOS"
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

Obtendrás los Links:

self: desde esta URL puedes consultar la información del pago.
approval_url: debes desplegar esta URL al cliente para que pueda continuar con el pago.
refund_method: te permite anular la transacción.
self_by_gateway_order: desde esta URL también puedes consultar la información del pago utilizando el gateway_order.

##Consultar la información de la transación:

Cuando se realiza una búsqueda para transacción se obtienen estos datos: 


```
{
     "_id": "5ca4ea4157a18100167f15de",
     "application": "5b76f2ef3eb77128dda44168",
     "purchase_order": {
       "purchase_order_id": "536155295217"
     },
     "additional_attributes": {
       "point_type": "CMR_PUNTOS"
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

## Anular o reversar una compra.

Para anular o reversar una compra, se debe usar el método refund o void. Al anular obtendremos un json de respuesta exitosa, en caso de que la anulación funcine de forma acorrecta, obtendremos un json como el siguiente.
En caso de que la anulación el refund falle, obtendremos los repsectivos mensajes de error.

```
{
  "_id": "5ca5044657a18100167f15fd",
  "application": "5b76f2ef3eb77128dda44168",
  "gateway": {
    "refunds": [
      {
        "refunded_amount": 100,
        "message": "successful refund",
        "refundResponseCode": 0,
        "refundResponseDescription": "Success",
        "refundCancellationCode": "168817647126",
        "refundTxnId": "3062450",
        "type": "CreditPayment"
      },
      {
        "refunded_amount": 10,
        "message": "successful refund",
        "refundResponseCode": 0,
        "refundResponseDescription": "Success",
        "refundTxnId": "3062451",
        "type": "PointsPayment"
      }
    ],
    "postMessage": {
      "msgType": "PayWithPointsResponse",
      "responseCode": 0,
      "responseDescription": "Success",
      "UUID": "4f99a1e7-69ae-4d3c-be4b-5823bc993b5e",
      "transactionId": "4f99a1e7-69ae-4d3c-be4b-5823bc993b5e"
    },
    "status": {
      "uuid": "4f99a1e7-69ae-4d3c-be4b-5823bc993b5e",
      "status": "DONE_POINTS",
      "errorDescription": "",
      "paymentTransactionDetails": [
        {
          "status": "success",
          "authorizationCode": "168817647122",
          "type": "CreditPayment",
          "qpTxnId": 3062448,
          "amount": 100,
          "accountFirst6": "111125",
          "accountLast4": "1713"
        },
        {
          "status": "success",
          "authorizationCode": "552256755111",
          "type": "PointsPayment",
          "qpTxnId": 3062449,
          "amount": 10
        }
      ],
      "createdDate": "2019-04-03T19:06:57.764Z",
      "updatedDate": "2019-04-03T19:08:19.160Z",
      "logTrackId": "#LGID=8a71335c7ab92ce1db13b8c11a317ada#MID=008598176#CHID=WEB#PYMT=P#DT=RUT#DID=177694886#UUID=4f99a1e7-69ae-4d3c-be4b-5823bc993b5e#TID=IP-15543184064832051#"
    },
    "resume": {
      "response": {
        "code": 0
      },
      "transaction": {
        "installments_number": 1,
        "points_amount": 10,
        "amount": 0,
        "buy_order": "IP-15543184064832051",
        "currency": "LOY",
        "date": "2019-04-03T19:08:20.567Z",
        "type": "CREDIT",
        "gateway_id": "4f99a1e7-69ae-4d3c-be4b-5823bc993b5e"
      },
      "authorizations": {
        "code": "168817647122"
      },
      "_id": "5ca504a44fec1e0016a6d753"
    }
  },
  "purchase_order": {
    "purchase_order_id": "536155295217"
  },
  "additional_attributes": {
    "point_type": "CMR_PUNTOS"
  },
  "redirect_urls": {
    "return_url": "http://portal.sandbox.connect.fif.tech",
    "cancel_url": "http://portal.sandbox.connect.fif.tech"
  },
  "transaction": {
    "gateway_order": "IP-15543184064832051",
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
      "email": "jhondoe@gmail.com",
      "full_name": "Jhon Doñe",
      "country": "CL",
      "document_number": "177694886",
      "document_type": "RUT"
    },
    "payment_method": "CMR_POINTS"
  },
  "links": [
    {
      "href": "https://api.qa.peinau.fif.tech/checkout/payments/5ca5044657a18100167f15fd",
      "rel": "self",
      "method": "GET"
    },
    {
      "href": "https://api.qa.peinau.fif.tech/checkout/payments/gateways/cmr/points/5ca5044657a18100167f15fd/pay",
      "rel": "approval_url",
      "method": "REDIRECT"
    },
    {
      "href": "https://api.qa.peinau.fif.tech/checkout/payments/5ca5044657a18100167f15fd/edit",
      "rel": "update_url",
      "method": "PUT"
    },
    {
      "href": "https://api.qa.peinau.fif.tech/checkout/payments/gateways/cmr/points/5ca5044657a18100167f15fd/void",
      "rel": "void_method",
      "method": "POST"
    },
    {
      "href": "https://api.qa.peinau.fif.tech/checkout/payments/gateways/cmr/points/5ca5044657a18100167f15fd/refund",
      "rel": "refund_method",
      "method": "POST"
    }
  ],
  "update_time": "2019-04-03T19:15:05.896Z",
  "create_time": "2019-04-03T19:06:46.483Z",
  "invoice_number": "IP-15543184064832051",
  "state": "refunded",
  "intent": "sale",
  "id": "5ca5044657a18100167f15fd"
}
```