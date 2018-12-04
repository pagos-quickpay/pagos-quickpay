Una vez hecha la intención de captura se procede a tokenizar con los datos de la tarjeta, nuevamente incluyendo el token de autorización en la cabecera del request.


```
{
 "user": {
   "country": "CL",
   "documentType": "RUT",
   "documentId": "371119582"
 },
 "panNumber": "4455961234561434"
}
```

Como respuesta obtendrás la siguiente información:

```
{
    "additional_attributes": {
        "remember_capture": false
    },
    "gateway": {
        "panLast4": "1434",
        "panFirst6": "445596",
        "qpCardId": "1111912816528678",
        "category": "|||",
        "status": "S"
    },
    "_id": "ad76140d-fcb7-48bc-9d80-986e85bd1261",
    "capture": "CMR_CAPTURE",
    "capture_method": "TOKENIZATION",
    "application": "5af350553dbed900146c5945",
    "links": [
        {
            "href": "https://api.qa.peinau.fif.tech/tokenization/captures/ad76140d-fcb7-48bc-9d80-986e85bd1261",
            "rel": "self",
            "method": "GET",
            "security": []
        },
        {
            "href": "https://api.qa.peinau.fif.tech/tokenization/captures/gateways/cmr/capture/ad76140d-fcb7-48bc-9d80-986e85bd1261/capture",
            "rel": "capture",
            "method": "POST",
            "security": [
                "Jwt"
            ]
        }
    ],
    "redirect_urls": {
        "return_url": "https://requestb.in/sfoogtsf",
        "cancel_url": "http://www.mysite.cl/cancel"
    },
    "billing": {
        "line1": "Miraflores 222",
        "city": "Santiago",
        "state": "Region Metropolitana",
        "country": "CL"
    },
    "cardholder": {
        "reference_id": "001389",
        "country": "CL",
        "name": "Jhon Doe",
        "email": "jhdoe@gmail.com"
    },
    "deletion_time": "2018-12-04T20:52:03.072Z",
    "update_time": "2018-12-03T20:52:13.898Z",
    "create_time": "2018-12-03T20:52:03.072Z",
    "state": "captured",
    "invoice_number": "INCA-1543870323072",
    "id": "ad76140d-fcb7-48bc-9d80-986e85bd1261"
}

```

Datos importantes:

- **gateway**: Contiene informacion del resultado de la tokenizacion, como el qpCardId, que es el token interno que utiliza quickpay para operar.
- **id**: es el token de Connect, con este token se debe proseguir a crear la intencion de pago para de este modo enlazar la intención de pago con la captura realizada
