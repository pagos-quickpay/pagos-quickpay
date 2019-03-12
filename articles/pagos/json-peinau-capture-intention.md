## Crear Intención de captura

## Ejemplo petición capture": "PEINAU_CAPTURE"

```
curl -X POST \
  https://api.qa.connect.fif.tech/tokenization/captures \
  -H 'authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJwcmltYXJ5c2lkIjoiMjhhZGI5OTktN2EyZS03MGI4LWMwOTItZTRjMTZhOWU5ZTBhIiwidW5pcXVlX25hbWUiOiJUb2lwYXRvLmNvbSIsImdyb3Vwc2lkIjoiQVBQTCIsImlzcyI6IkZhbGFiZWxsYSIsImF1ZCI6IldlYiIsInR5cGUiOiJCZWFyZXIiLCJzY29wZSI6W10sImlhdCI6MTUxMzE3Nzk1OCwiZXhwIjoxNTEzMTc4ODU4fQ.OYBksNEvNBU012fJt4IhUnQ5g0szPXPmivD2GvprLczjbG6Pd7HeSyWddSCVOAwAXfycNMzwn0nb_6VdYMqbSzE3T9Bu0Oqzih4b_BfLLb4EwpRQ3L0ObFNkJTI2hfIMUNJQ5ohT8b2yR-1SiehAUd0Tlkb3zrh2aDP9AYVZGqkjLdnwQOpBtXVs6VmntXnb3_MklOU7U0BylB1kVG40t9qfSxf79DYTcr3JWs6LdCFDThkudMZtJfnjYsOoqt--Iv8BzhCU7Eft1Isf2Qfqn_1-p778E7r4yQY1GREuAsXPNfnnHxi7gOVVQ1owq1aekqt4m4ML-VLow8pUx5duYw' \
  -H 'content-type: application/json' \
  -d ' {
  "capture": "PEINAU_CAPTURE",
  "capture_method": "TOKENIZATION",
  "cardholder": {
    "reference_id": "Merchant_id_reference",
    "name": "Jhon Doe",
    "email": "jhondoe@gmail.com",
    "country": "CL"
  },
  "billing": {
    "line1": "Miraflores 222",
    "city": "Santiago",
    "state": "Region Metropolitana",
    "country": "CL"
  },
  "redirect_urls": {
    "return_url": "http://www.micomercio.com/success",
    "cancel_url": "http://www.micomercio.com/fail"
  }
}'
 ```

Como respuesta obtendrás la siguiente información:

```
{
    "capture": "PEINAU_CAPTURE",
    "capture_method": "TOKENIZATION",
    "application": "5ae7359a6a3635000fafbc4c",
    "links": [
        {
            "href": "https://api.qa.peinau.fif.tech/tokenization/captures/6def20e2-28d0-4612-8f53-634990982a14",
            "rel": "self",
            "method": "GET",
            "security": []
        },
        {
            "href": "https://api.qa.peinau.fif.tech/tokenization/captures/gateways/peinau/capture/6def20e2-28d0-4612-8f53-634990982a14/capture",
            "rel": "capture_url",
            "method": "REDIRECT",
            "security": []
        },
        {
            "href": "https://api.qa.peinau.fif.tech/tokenization/captures/gateways/peinau/capture/6def20e2-28d0-4612-8f53-634990982a14/capture",
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
    "deletion_time": "2019-03-12T15:12:29.540Z",
    "update_time": "2019-03-12T15:07:29.540Z",
    "create_time": "2019-03-12T15:07:29.540Z",
    "state": "created",
    "invoice_number": "INCA-1552403249540",
    "_id": "6def20e2-28d0-4612-8f53-634990982a14",
    "id": "6def20e2-28d0-4612-8f53-634990982a14"
}
```

**Obtendrás los Links:**

- **self**: desde esta URL puedes consultar la información de la captura. [Ejemplo de ejecución de Self](self-capture.md).
- **capture_url**: con esta URL podemos abrir el iframe para tokenizar la tarjeta. [Ejemplo de apertura de iframe de tokenización](json-iframe-capture.md).
- **capture_card**: este endpoint sirve para tokenizar la tarjeta enviando sus datos (para utilizar esta opción, el comercio debe tener certificación PCI). [Ejemplo de ejecución del capture/tokenización](json-capture.md).

> Estas URLs son dinamicas, nunca debes guardarlas como variables de entorno. Siempre debes consultarlas desde aquí para continuar con los pasos siguientes.
