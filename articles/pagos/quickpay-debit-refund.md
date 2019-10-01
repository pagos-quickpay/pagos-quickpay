## Ejemplo petición de devolución:

Para devolver el dinero al cliente se debe invocar el endpoint rel: “refund_method”. Ejemplo

```
 curl -X POST 'https://api.qa.peinau.fif.tech/checkout/payments/gateways/quickpay/debit/5c1034ee0b16c80015ae0cd7/refund' \
  -H 'authorization: Bearer REEMPLAZAR AQUI EL ACCESS TOKEN' \
  -H 'content-type: application/json' \
  -d '{
	"refunded_amount":"1000",
	"items": [{
		"sku": "117110",
		"quantity": 1
	}]
       }'
```
El campo "items" es opcional. Además, las anulaciones pueden ser parciales enviando en el campo "refunded_amount" un valor menor al valor autorizado.
 
A continuación se presenta ejemplo de un JSON de respuesta obtenido al devolver una intención de pago a través de la API RESTful de checkout:

```
{  
   "_id":"5c1034ee0b16c80015ae0cd7",
   "application":"5af0799cd1aa8e000f9de4ca",
   "purchase_order":{  
      "purchase_order_date":"2018-12-11T00:00:00-05:00",
      "purchase_order_id":"0483758493007"
   },
   "additional_attributes":{  
      "is_deferred_capture":"false",
      "default_deferred_month":"0",
      "default_installment_number":"1",
      "installments_without_interest":[  
         "2"
      ]
   },
   "redirect_urls":{  
      "return_url":"https://www.falabella.com",
      "cancel_url":"https://www.google.com"
   },
   "transaction":{  
      "gateway_order":"IP-15445659981836191",
      "reference_id":null,
      "description":"Transaction in app 789156083925170982900platform  QPAY id 0dfbb32c-2234-46e5-9e92-561511c00623",
      "soft_descriptor":"id 0dfbb32c-2234-46e5-9e92-561511c00623",
      "item_list":{  
         "shipping_method":"PICK_IN_PLACE",
         "items":[  
            {  
               "sku":"117110",
               "name":"Cordu00f3n 3x1 mm 10 m metro lineal Negro",
               "description":"Cordu00f3n 3x1 mm 10 m metro lineal Negro",
               "quantity":1,
               "price":7200,
               "tax":0
            }
         ],
         "shipping_address":{  
            "line1":"Av. Las Condes 11049, Las Condes",
            "city":"Chile",
            "country_code":"CL",
            "phone":"+56956821215",
            "type":"HOME_OR_WORK",
            "recipient_name":"Alejandro Rivero "
         }
      },
      "amount":{  
         "currency":"CLP",
         "total":1000,
         "details":{  
            "subtotal":1000,
            "tax":0,
            "shipping":0,
            "shipping_discount":0
         }
      }
   },
   "payer":{  
      "payer_info":{  
         "is_guest":"true",
         "document_type":"RUT",
         "document_number":"134918942",
         "country":"CL",
         "full_name":"Alejandro Rivero",
         "email":"dummy@gmail.com"
      },
      "payment_method":"QUICKPAY_DEBIT"
   },
   "links":[  
      {  
         "href":"https://api.qa.peinau.fif.tech/checkout/payments/5c1034ee0b16c80015ae0cd7",
         "rel":"self",
         "method":"GET"
      },
      {  
         "href":"https://api.qa.peinau.fif.tech/checkout/payments/gateways/quickpay/debit/5c1034ee0b16c80015ae0cd7/pay",
         "rel":"approval_url",
         "method":"REDIRECT"
      },
      {  
         "href":"https://api.qa.peinau.fif.tech/checkout/payments/5c1034ee0b16c80015ae0cd7/edit",
         "rel":"update_url",
         "method":"PUT"
      },
      {  
         "href":"https://api.qa.peinau.fif.tech/checkout/payments/gateways/quickpay/debit/5c1034ee0b16c80015ae0cd7/void",
         "rel":"void_method",
         "method":"POST"
      },
      {  
         "href":"https://api.qa.peinau.fif.tech/checkout/payments/gateways/quickpay/debit/5c1034ee0b16c80015ae0cd7/refund",
         "rel":"refund_method",
         "method":"POST"
      }
   ],
   "update_time":"2018-12-11T22:08:45.751Z",
   "create_time":"2018-12-11T22:06:38.183Z",
   "invoice_number":"IP-15445659981836191",
   "state":"refunded",
   "intent":"sale",
   "billing_address":{  

   },
   "gateway":{  
      "refunds":[  
         {  
            "refunded_amount":1000,
            "message":"successful refund",
            "refundResponseCode":0,
            "refundResponseDescription":"Success",
            "refundCancelationCode":"92873459",
            "refundTxnId":"2443776"
         }
      ],
      "msgType":"DebitResponse",
      "responseCode":0,
      "responseDescription":"Success",
      "responseSignature":"9bwv8idJjrXFBorAlGqvtOs+Lb4t2coKThShsYYonZM=",
      "payerUserProfile":null,
      "logTrackId":"#LGID=20862351f592bca7250a1f34a4462719#MID=005333110#CID=WEB#PYMT=D#DT=RUT#DID=134918942#",
      "riskEngineFinalResult":"0",
      "qpTxnId":2443775,
      "authorizationCode":"92873458",
      "resume":{  
         "response":{  
            "code":0
         },
         "transaction":{  
            "installments_number":0,
            "amount":1000,
            "buy_order":"IP-15445659981836191",
            "currency":"CLP",
            "date":"2018-12-11T22:06:56.204Z",
            "type":"DEBIT",
            "gateway_id":"2443775"
         },
         "authorizations":{  
            "code":"92873458"
         },
         "_id":"5c1035007e83c80015bbb9e9"
      }
   },
   "meta_data":{  

   },
   "shipping_list":{  

   },
   "travel":{  

   }
}
```


