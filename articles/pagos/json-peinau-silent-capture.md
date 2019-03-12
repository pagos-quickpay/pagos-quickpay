Una vez hecha la intención de captura se procede a capturar/tokenizar con los datos de la tarjeta, nuevamente incluyendo el token de autorización en la cabecera del request.


```
{
  "card_number": "4111111111111111",
  "expiry_month": "2",
  "expiry_year": "2020",
  "card_ccv": "123"
}
```

Como respuesta obtendrás la siguiente información:

```
{
    "additional_attributes": {
        "remember_capture": false
    },
    "gateway": {
        "req_card_number": "xxxxxxxxxxxx1111",
        "payment_token": "5524046972316167604008",
        "panLast4": "1111",
        "panFirst6": "411111",
        "additionalProcessorResponse": "92e8c29b-08d1-48dd-ba4b-b6b439158741",
        "paySubscriptionCreateReply": {
            "subscriptionID": "5524046972316167604008",
            "reasonCode": "100"
        },
        "ccCaptureReply": {
            "reconciliationID": "SWXPGRBFJSU0G8OT",
            "amount": "10",
            "requestDateTime": "2019-03-12T15:31:37Z",
            "reasonCode": "100"
        },
        "ccAuthReply": {
            "processorTransactionID": "be1bed1b836148798bf859a7eac95de3",
            "paymentNetworkTransactionID": "111222",
            "reconciliationID": "SWXPGRBFJSU0G8OT",
            "processorResponse": "1",
            "authorizedDateTime": "2019-03-12T15:31:37Z",
            "cvCode": "3",
            "avsCode": "1",
            "authorizationCode": "570110",
            "amount": "10",
            "reasonCode": "100"
        },
        "purchaseTotals": {
            "currency": "CLP"
        },
        "requestToken": "Ahj//wSTK3WNPaqVQocoiiFOvYoR6UKNKp1WEdxPqKNPxHryCAVGn4j15BEwEqNvhk0ky9GK6rTwMCcmVusae1UqhQ5QAAAAKQZu",
        "reasonCode": "100",
        "decision": "ACCEPT",
        "requestID": "5524046972316167604008",
        "merchantReferenceCode": "Merchant_id_reference"
    },
    "_id": "0dae14f4-7da0-4cf5-8b7c-41903fab87bd",
    "capture": "PEINAU_CAPTURE",
    "capture_method": "TOKENIZATION",
    "application": "5ae7359a6a3635000fafbc4c",
    "links": [
        {
            "href": "https://api.qa.peinau.fif.tech/tokenization/captures/0dae14f4-7da0-4cf5-8b7c-41903fab87bd",
            "rel": "self",
            "method": "GET",
            "security": []
        },
        {
            "href": "https://api.qa.peinau.fif.tech/tokenization/captures/gateways/peinau/capture/0dae14f4-7da0-4cf5-8b7c-41903fab87bd/capture",
            "rel": "capture_url",
            "method": "REDIRECT",
            "security": []
        },
        {
            "href": "https://api.qa.peinau.fif.tech/tokenization/captures/gateways/peinau/capture/0dae14f4-7da0-4cf5-8b7c-41903fab87bd/capture",
            "rel": "capture_card",
            "method": "POST",
            "security": [
                "Jwt"
            ]
        }
    ],
    "redirect_urls": {
        "return_url": "http://www.micomercio.com/success",
        "cancel_url": "http://www.micomercio.com/fail"
    },
    "billing": {
        "line1": "Miraflores 222",
        "city": "Santiago",
        "state": "Region Metropolitana",
        "country": "CL"
    },
    "cardholder": {
        "reference_id": "Merchant_id_reference",
        "name": "Jhon Doe",
        "email": "jhondoe@gmail.com",
        "country": "CL"
    },
    "deletion_time": "2019-03-13T15:31:26.603Z",
    "update_time": "2019-03-12T15:31:37.850Z",
    "create_time": "2019-03-12T15:31:26.603Z",
    "state": "captured",
    "invoice_number": "INCA-1552404686603",
    "id": "0dae14f4-7da0-4cf5-8b7c-41903fab87bd"
}

```

Datos importantes:

- **gateway**: Contiene informacion del resultado de la tokenizacion.
- **state**: Estado final de la captura (**captured** / **rejected**)
- **id**: es el token de Connect, con este token se debe proseguir a crear la intencion de pago para de este modo enlazar la intención de pago con la captura realizada
