## Assess Fraud Risk
Antes de llamar a la url, es preciso indicar que para poder realizar una validación de fraude con Cybersource, debes haber creado una intención de pago enviando más atributos de los que comunmente enviarías en una intención de pago. A continuación, creamos la intención de pago.

```
curl -X POST \
  https://api.qa.peinau.fif.tech/checkout/payments \
  -H 'authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJwcmltYXJ5c2lkIjoiMjhhZGI5OTktN2EyZS03MGI4LWMwOTItZTRjMTZhOWU5ZTBhIiwidW5pcXVlX25hbWUiOiJUb2lwYXRvLmNvbSIsImdyb3Vwc2lkIjoiQVBQTCIsImlzcyI6IkZhbGFiZWxsYSIsImF1ZCI6IldlYiIsInR5cGUiOiJCZWFyZXIiLCJzY29wZSI6W10sImlhdCI6MTUxMzE3Nzk1OCwiZXhwIjoxNTEzMTc4ODU4fQ.OYBksNEvNBU012fJt4IhUnQ5g0szPXPmivD2GvprLczjbG6Pd7HeSyWddSCVOAwAXfycNMzwn0nb_6VdYMqbSzE3T9Bu0Oqzih4b_BfLLb4EwpRQ3L0ObFNkJTI2hfIMUNJQ5ohT8b2yR-1SiehAUd0Tlkb3zrh2aDP9AYVZGqkjLdnwQOpBtXVs6VmntXnb3_MklOU7U0BylB1kVG40t9qfSxf79DYTcr3JWs6LdCFDThkudMZtJfnjYsOoqt--Iv8BzhCU7Eft1Isf2Qfqn_1-p778E7r4yQY1GREuAsXPNfnnHxi7gOVVQ1owq1aekqt4m4ML-VLow8pUx5duYw' \
  -H 'content-type: application/json' \
  -d ' {
  "intent": "sale",
  "payer": {
    "payer_info": {
      "email": "reject@reject.com",
      "first_name": "Marta",
      "last_name": "Larracheava",
      "country": "PE",
      "document_number": "47007107",
      "document_type": "DNI",
      "qp_user_id": "",
      "phone": "56987861255",
      "is_guest": "false",
      "gender": "Male",
      "age": "55",
      "session_attempt_count": "1",
      "taxpayer_identity": "2343243242",
      "ip": "200.10.10.10",
      "category": "Elite",
      "is_employee": "true",
      "session_id": "12ADAsfs2333"
    },						
    "payment_method": "QUICKPAY_CREDIT"
  },
  "transaction": {
  	"gift_card": "false",
    "reference_id": "OD0000233",
    "description": "Transaction detailed description",
    "soft_descriptor": "Transaction Short description",
    "associate_promotion": "Prueba2050",
    "receipt_type": "Factura",
    "with_discount_coupon": "true",
    "amount": {
      "currency": "PEN",
      "total": 111,
      "details": {
        "subtotal": 1000,
        "tax": 0,
        "discount_percentage": "10",
        "shipping": 0,
        "shipping_discount": 0
      }
    },
    "item_list": {
      "shipping_address": {
        "line1": "General Carol Urzua 1020, Depto 102A",
        "city": "Santiago",
        "country_code": "PE",
        "phone": "+56 9 8762 1244",
        "type": "HOME_OR_WORK",
        "recipient_name": "Jhon Doe Son"
      },
      "shipping_method": "DIGITAL",
      "items": [
        {
          "thumbnail": "http://portal.sandbox.connect.fif.tech/bundles/app/css/images/e-commerce-demo/product-icon.png",
          "sku": "TRK345-2",
          "category": "Viaje Intercontinental",
          "name": "Flight 2344",
          "description": "Default",
          "quantity": 2,
          "price": 500,
          "tax": 0
        }
      ]
    }
  },
  "travel": {
    "complete_route": "ESP-ITA",
    "departure_datetime": "2019-09-18T12:35:31",
    "journey_type": "IdaVuelta",
    "passenger_count": "3",
    "passengers": [
      {
        "first_name": "Oswaldo",
        "last_name": "Garcia",
        "phone": "987987987",
        "email": "juanitoperez@gmail.com",
        "document_id": "876123",
        "document_type": "DNI",
        "status": "VIP",
        "country": "PE",
        "type": "Cnn"
      }
    ]
  },
  "redirect_urls": {
    "return_url": "https://falabella.com",
    "cancel_url": "http://portal.sandbox.connect.fif.tech"
  },
  "additional_attributes": {
  	"capture_token": "{{token_intencion_captura}}",
  	"total_product_count": "10",
  	"enrollment_days": "10",
	"channel": "FONO_COMPRAS",
 	"afrInputs": [
	  {
		"id": "52",
		"value": "PEFA4562135"
	  },
	  	  {
		"id": "72",
		"value": "PEFA4562235"
	  }
    ], 
    "wedding_code": "false",
    "customer_registration_days": "2014-10-15T00:00:00",
    "first_purchase_days": "901820",
   
    "default_installment_number": "8",
    "default_deferred_month": "1",
    "is_deferred_capture": "true",
    "last_purchase_days": "20",
    "customer_purchases_number": "3",
    "purchase_history": "1",
    "average_purchases_amount": "12.33",
    "average_purchases_time": "1234",
    "is_save_card_customer": "true", 
    "is_save_card_payment": "true", 
    "other_card_attempts": "2", 
    "origin_phone_number": "987987987",
    "copy_paste_email": "false",
    "email_confirmed": "true",
	"changed_register": "false",
    "days_change_register": "5",
    "phone_confirmed": "true",
    "seller_name": "Armando Guerra",
    "modified_order": "false",
    "is_no_food": "true",
    "copy_paste_card": "false",
    "commerce_risk_data": "R999",
    "credit_cards_count": "2",
    "device_finger_print": "123456rrra"
  },
  "shipping_list": {
    "shipping": {
      "line1": "Nueva York 54",
      "city": "Lima",
      "state": "MIraflores",
      "postal_code": "801010",
      "country": "PE",
      "commune": "SANTIAGO",
      "county": "RM",
      "region": "RM", 
      "document_type": "DNI",
      "document_number": "10321050",
      "first_name": "Andres",
      "last_name": "Roa",
      "phone": "56987861255",
      "store_id": "999",
      "date": "2019-08-26T00:00:00-03:00",
      "pick_up_type": "terceros",
      "is_pickup":"false",
      "type": "DESPACHO_NOVIOS",
      "shipping_way": "Motoboy",
      "courier_name": "Fedex"
    }
  },
  "purchase_order": {
    "purchase_order_id": "7896",
    "purchase_order_date": "2019-08-23T00:00:00-05:00"
  },
  "billing_address": {
    "address": "Agustinas 445",
    "city": "Santiago",
    "state": "RM",
    "postal_code": "800088",
    "country": "PE",
    "commune": "SANTIAGO",
    "county": "RM",
    "region": "RM"
  }
}'
 
```
A continuación, se adjunta el archivo con el detalle de los campos que utiliza el servicio AFR. (Seleccionar "Descargar")[Excel](Campos_formato_AFR.xlsx)

Importante a destacar que debes enviar el capture_token que fue recibido como parte de la captura hecha previamente. Después de crear la intención de pago.

Ahora sí se puede llamar a la url de Assess Fraud Risk. A continuación un ejemplo.

```
curl -X GET \
  https://api.qa.peinau.fif.tech/checkout/payments/gateways/quickpay/credit/5d2f86cc160cd40016372c51/assessFraudRisk \
  -H 'Authorization: Bearer ACCESS_TOKEN'
```
**Respuesta**
La respuesta de validación de fraude se graba en el documento de intención de pago en el atributo gateway.afr:

```
    "gateway": {
        "afr": {
            "BaseHeader": {
                "responseDesc": "Success",
                "responseCode": 0
            },
            "AssessFraudRiskRes": {
                "cybersourceCaseNumber": "5633974381756704504009",
                "cybersourceDescription": "ACCEPT",
                "cybersourceCode": "100",
                "riskStatus": "SAFE"
            }
        }
    },
```

**Respuesta ACCEPT**
En ambiente de QA, podemos forzar una respuesta "ACCEPT", enviando en el correo del pagador (atributo payer.payer_info.email) el valor "**accept@accept.com**". Con lo cual, obtendremos la siguiente respuesta:

```
"afr": {
    "BaseHeader": {
	"responseDesc": "Success",
	"responseCode": 0
    },
    "AssessFraudRiskRes": {
	"cybersourceCaseNumber": "5633974381756704504009",
	"cybersourceDescription": "ACCEPT",
	"cybersourceCode": "100",
	"riskStatus": "SAFE"
    }
}
```

**Respuesta REVIEW**
En ambiente de QA, podemos forzar una respuesta "REVIEW", enviando en el correo del pagador (atributo payer.payer_info.email) el valor "**review@review.com**". Con lo cual, obtendremos la siguiente respuesta:

```
"afr": {
    "BaseHeader": {
	"responseDesc": "Success",
	"responseCode": 0
    },
    "AssessFraudRiskRes": {
	"cybersourceCaseNumber": "5633999467026951704008",
	"cybersourceDescription": "REVIEW",
	"cybersourceCode": "480",
	"riskStatus": "VERIFY"
    }
}
```

**Respuesta REJECT**
En ambiente de QA, podemos forzar una respuesta "REJECT", enviando en el correo del pagador (atributo payer.payer_info.email) el valor "**reject@reject.com**". Con lo cual, obtendremos la siguiente respuesta:

```
"afr": {
    "BaseHeader": {
	"responseDesc": "Success",
	"responseCode": 0
    },
    "AssessFraudRiskRes": {
	"cybersourceCaseNumber": "5633990169686874404007",
	"cybersourceDescription": "REJECT",
	"cybersourceCode": "481",
	"riskStatus": "REJECT"
    }
}
```

**Otros errores**
En caso no hayas enviado alguno de los campos anteriormente mencionados, podras obtener un error de signature:

```
"afr": {
    "BaseHeader": {
	"responseDesc": "Invalid Signature",
	"responseCode": 1
    }
}
```

[Regresar](json-captured-quickpay-credit.md)
