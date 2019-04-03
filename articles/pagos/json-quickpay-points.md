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
**Consultar el estado de la transación:**

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