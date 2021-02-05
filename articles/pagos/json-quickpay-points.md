## Ejemplo petición payment_method": "CMR_POINTS"
Para CMR_POINTS la app permite usuarios clientes  y no clientes tanto para Chile, Colombia y Perú.
Teniendo como opción canje de puntos y puntos más pesos, este ultimo solo para clientes CMR. 

Ejemplos para canje de  puntos, se debe sestear el total en cero ya que no acepta puntos más pesos (opción que aplica para no clientes Chile, clientes y no clientes Colombia y Perú).
```
"amount": {
    "currency": "CLP",
    "total": 0,
    "details": {
      "subtotal": 0,
      "tax": 0,
      "shipping": 0,
      "shipping_discount": 0
    }
  },
```
Ejemplo para puntos más pesos, opción que permite solo a clientes Chile 
```
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
  ``` 
 A continuación se muestra la petición completa 
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
  },
  "gateway_order": "900000065434"
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
| "true"              | Viene (opcional)	        | No viene      | N/A                          | Se pide primer factor y se muestra  tipo de documento por defecto, se permite cambio de   tipo de documento y/o número de documento este ultimo aplicando para CO-PE|
| "true"              | Viene (opcional)	        | Viene         | < 3 minutos		       | Se omite la autenticación del primer factor|
| "true"              | Viene (opcional)	        | Viene		| > 3 minutos		       | Se pide primer factor y se muestra tipo de documento por defecto, se permite cambio de  tipo de documento y/o número de documento este ultimo aplicando para CO-PE |
| "true"              | No viene (opcional)		| Viene         | < 3 minutos		       | Se omite la autenticación de primer factor (Payments obtiene tipo de documento de intención de consulta)|
| "true" 	      | No viene (opcional)     	| Viene		| > 3 minutos		       | Se pide primer factor y tipo de documento y/o número de documento este ultimo aplicando para CO-PE |
| "true"              | No viene (opcional) 	        | No viene 	| N/A 			       |Se pide primer factor y tipo de documento y/o número de documento este ultimo aplicando para CO-PE |
| "false" 	      | Viene (obligatorio)		| No viene	| N/A			       | Se omite la autenticación de primer factor|
| "false"	      | Viene (obligatorio)		| Viene		| < 3 minutos		       | Se omite la autenticación de primer factor|
| "false"	      | Viene (obligatorio)		| Viene		| > 3 minutos		       | Se omite la autenticación de primer factor|
| "false"	      | No viene (obligatorio)		| Viene		| < 3 minutos		       | Devolvemos un error |
| "false"	      | No viene (obligatorio)		| Viene		| > 3 minutos		       | Devolvemos un error |
| "false"	      | No viene (obligatorio)		| No viene	| N/A			       | Devolvemos un error |

Es importante mencionar que se parametrizaron los valores para el envío del segundo factor según puntos por país (Lógica solo para canje de puntos)

|**País**             | **Parametrización** |
|-------------------  | --------------------|
|Chile                | 0 puntos            |
|Colombia             | 9.000 puntos        |
|Perú                 | 9.000 puntos        |

 Se ríge bajo los siguentes atributos 

| **is_guest**         | **Parametrización** | **Acción**                                                                         |
| -------------------  | --------------------| -----------------------------------------------------------------------------------|
| False                |  > 9.000            | Realizar canje directo sin solicitar autenticación                                 |
| False                |  ≤ 9.000            | Pasa directo y solicita segundo factor                                             |

Tabla que representa el país y su respectivo tipo de documento 

| **País**            | **Tipo de documento**           |
| ------------------- | ------------------------------- | 
|Chile                | Rut
|Colombia             | Cédula de ciudadanía            |
|                     | Cédula de extranjería           | 
|Perú                 | DNI                             | 
|                     | Carnet de extranjería           | 

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

preventive_void_method: Permite cancelar la transacción, cuando debido a un error de comunicación, el estado de la intención no se actualizó a paid

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
## Mostrar Formulario Pago con puntos más pesos

Con la **approval_url** de la respuesta de la intención de captura, puedes iniciar el flujo de pago de puntos/puntos más pesos

**Canje de puntos más pesos, opción que aplica solo para clientes Chile**

![Ejmplo de Apertura  ppmp de pago](images/cpmp1.png)

El cliente debe ingresar los datos “tipo de documento (Rut) y multiclave” seleccionar las cuotas, pasar la prueba de segundo factor y aprobar el pago para que nuestro sistema pueda ejecutar la carga a la tarjeta de crédito.

**Canje de puntos no clientes Chile**

![Ejmplo de Apertura cnc  de pago](images/cnc.2.png)

Un no cliente debe ingresar los datos tipo de documento (Rut) y multiclave, pasar la prueba de segundo factor donde si es primera vez que se auténtica, se solicitará la validación por TransUnion lo que deberá ingresar el número de serie del carnet para realizar el canje

**Canje de puntos Cliente Banco falabella Colombia** 

![Ejmplo de Apertura ccc  de pago](images/ccc.2.png)

El cliente debe ingresar los datos tipo de documento desplegando el combobox, número de documento y multiclave, pasar la prueba de segundo factor para realizar el canje

**Canje de puntos de un No cliente Perú**

![Ejmplo de Apertura cncp  de pago](images/cncp.2.png)

El cliente debe ingresar los datos tipo de documento desplegando el combobox, número de documento y multiclave, pasar la prueba de segundo factor para realizar el canje

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

## Reversa preventiva.

La reversa preventiva se ejecuta cuando la intención esta en estado created. (La reversa preventiva solo se puede ejecutar una vez)

```
{
    "_id": "5fbc20724a5496001740535d",
    "application": "5f186a3f5f62bf0017a6042c",
    "gateway": {
        "void": [
            {
                "merchTxnId": "IP-16061645944853931-CMR",
                "code": "SUCCESSFUL_REVERSAL",
                "message": "successful reversal",
                "statusCode": 200
            }
        ],
        "postMessage": {
            "msgType": "PayWithPointsResponse",
            "responseCode": 0,
            "responseDescription": "Success",
            "UUID": "56f9941a-9e17-4e88-9bda-bd74d41c8dcf",
            "transactionId": "56f9941a-9e17-4e88-9bda-bd74d41c8dcf"
        },
        "status": {
            "uuid": "56f9941a-9e17-4e88-9bda-bd74d41c8dcf",
            "status": "DONE_POINTS",
            "errorDescription": "",
            "paymentTransactionDetails": [
                {
                    "status": "success",
                    "authorizationCode": "000000482133",
                    "type": "PointsPayment",
                    "qpTxnId": 7309961,
                    "amount": 5000
                }
            ],
            "createdDate": "2020-11-23T20:49:57.834Z",
            "updatedDate": "2020-11-23T20:50:10.007Z",
            "logTrackId": "#LGID=7f2ccfe1b6b529a6fe738c1e5d0f4b2d#MID=005751018#CHID=WEB#PYMT=P#DT=RUT#DID=148313148#UUID=56f9941a-9e17-4e88-9bda-bd74d41c8dcf#TID=IP-16061645944853931#",
            "documentNumber": "CL:RUT:148313148"
        },
        "resume": {
            "response": {
                "code": 0
            },
            "transaction": {
                "points_amount": 5000,
                "amount": 0,
                "buy_order": "IP-16061645944853931",
                "currency": "CMR",
                "date": "2020-11-23T20:50:10.688Z",
                "type": "POINTS",
                "gateway_id": "56f9941a-9e17-4e88-9bda-bd74d41c8dcf"
            },
            "authorizations": {
                "code": "000000482133"
            },
            "_id": "5fbc208222116f001efbe64b"
        }
    },
    "purchase_order": {
        "purchase_order_id": "536155295217CVC201"
    },
    "additional_attributes": {
        "point_type": "CMR_PUNTOS"
    },
    "redirect_urls": {
        "return_url": "http://localhost/experiences/ok",
        "cancel_url": "http://localhost/experiences/nok"
    },
    "transaction": {
        "gateway_order": "IP-16061645944853931",
        "description": "Transaction detailed description",
        "soft_descriptor": "Transaction Short description",
        "item_list": {
            "shipping_method": "DIGITAL",
            "items": [
                {
                    "thumbnail": "http://portal.sandbox.connect.fif.tech/bundles/app/css/images/e-commerce-demo/product-icon.png",
                    "sku": "000000000000000101",
                    "name": "Flight 2344",
                    "description": "Flight SCL - ONT",
                    "quantity": 1,
                    "price": 0,
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
            "total": 5000
        },
        "amount": {
            "currency": "CLP",
            "total": 0,
            "details": {
                "subtotal": 0,
                "tax": 0,
                "shipping": 0,
                "shipping_discount": 0
            }
        }
    },
    "payer": {
        "payer_info": {
            "email": "jhondoe@gmail.com",
            "full_name": "Jhon Doñe",
            "country": "CL",
            "document_number": "148313148",
            "document_type": "RUT",
            "is_guest": "false"
        },
        "payment_method": "CMR_POINTS"
    },
    "links": [
        {
            "href": "https://api.qa.peinau.fif.tech/checkout/payments/5fbc20724a5496001740535d",
            "rel": "self",
            "method": "GET"
        },
        {
            "href": "https://api.qa.peinau.fif.tech/checkout/payments/gateways/cmr/points/5fbc20724a5496001740535d/pay",
            "rel": "approval_url",
            "method": "REDIRECT"
        },
        {
            "href": "https://api.qa.peinau.fif.tech/checkout/payments/5fbc20724a5496001740535d/edit",
            "rel": "update_url",
            "method": "PUT"
        },
        {
            "href": "https://api.qa.peinau.fif.tech/checkout/payments/gateways/cmr/points/5fbc20724a5496001740535d/void",
            "rel": "void_method",
            "method": "POST"
        },
        {
            "href": "https://api.qa.peinau.fif.tech/checkout/payments/gateways/cmr/points/5fbc20724a5496001740535d/preventive-void",
            "rel": "preventive_void_method",
            "method": "POST"
        },
        {
            "href": "https://api.qa.peinau.fif.tech/checkout/payments/gateways/cmr/points/5fbc20724a5496001740535d/refund",
            "rel": "refund_method",
            "method": "POST"
        }
    ],
    "update_time": "2020-11-23T20:52:03.022Z",
    "create_time": "2020-11-23T20:49:54.485Z",
    "invoice_number": "IP-16061645944853931",
    "state": "preventive_voided",
    "intent": "sale",
    "id": "5fbc20724a5496001740535d"
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
