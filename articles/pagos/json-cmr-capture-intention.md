## Crear Intención de captura

## Ejemplo petición capture": "CMR_CAPTURE"

```
curl -X POST \
  https://api.qa.peinau.fif.tech/tokenization/captures \
  -H 'authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJwcmltYXJ5c2lkIjoiMjhhZGI5OTktN2EyZS03MGI4LWMwOTItZTRjMTZhOWU5ZTBhIiwidW5pcXVlX25hbWUiOiJUb2lwYXRvLmNvbSIsImdyb3Vwc2lkIjoiQVBQTCIsImlzcyI6IkZhbGFiZWxsYSIsImF1ZCI6IldlYiIsInR5cGUiOiJCZWFyZXIiLCJzY29wZSI6W10sImlhdCI6MTUxMzE3Nzk1OCwiZXhwIjoxNTEzMTc4ODU4fQ.OYBksNEvNBU012fJt4IhUnQ5g0szPXPmivD2GvprLczjbG6Pd7HeSyWddSCVOAwAXfycNMzwn0nb_6VdYMqbSzE3T9Bu0Oqzih4b_BfLLb4EwpRQ3L0ObFNkJTI2hfIMUNJQ5ohT8b2yR-1SiehAUd0Tlkb3zrh2aDP9AYVZGqkjLdnwQOpBtXVs6VmntXnb3_MklOU7U0BylB1kVG40t9qfSxf79DYTcr3JWs6LdCFDThkudMZtJfnjYsOoqt--Iv8BzhCU7Eft1Isf2Qfqn_1-p778E7r4yQY1GREuAsXPNfnnHxi7gOVVQ1owq1aekqt4m4ML-VLow8pUx5duYw' \
  -H 'content-type: application/json' \
  -d ' {
  "capture": "CMR_CAPTURE",
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
    "return_url": "http://portal.qa.connect.fif.tech",
    "cancel_url": "http://portal.qa.connect.fif.tech"
  }
}'
 ```

Como respuesta obtendrás la siguiente información:

```
{
    "capture": "CMR_CAPTURE",
    "capture_method": "TOKENIZATION",
    "application": "5af350553dbed900146c5945",
    "links": [
        {
            "href": "https://api.qa.peinau.fif.tech/tokenization/captures/ed72148e-3037-45e3-8ae3-e16eb4643a0f",
            "rel": "self",
            "method": "GET",
            "security": []
        },
        {
            "href": "https://api.qa.peinau.fif.tech/tokenization/captures/gateways/cmr/capture/ed72148e-3037-45e3-8ae3-e16eb4643a0f/capture",
            "rel": "capture_url",
            "method": "REDIRECT",
            "security": []
        },
        {
            "href": "https://api.qa.peinau.fif.tech/tokenization/captures/gateways/cmr/capture/ed72148e-3037-45e3-8ae3-e16eb4643a0f/capture",
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
        "reference_id": "Merchant_id_reference",
        "country": "CL",
        "name": "Jhon Doe",
        "email": "jhondoe@gmail.com"
    },
    "deletion_time": "2018-12-03T20:32:48.042Z",
    "update_time": "2018-12-03T20:27:48.041Z",
    "create_time": "2018-12-03T20:27:48.041Z",
    "state": "created",
    "invoice_number": "INCA-1543868868041",
    "_id": "ed72148e-3037-45e3-8ae3-e16eb4643a0f",
    "id": "ed72148e-3037-45e3-8ae3-e16eb4643a0f"
}
```

> **Recordar** que el plazo de tiempo para que una intención de captura sea tokenizada es de 5 minutos. Ver el ejemplo del JSON de respuesta a la creación de intención de captura en el que el atributo "deletion_time" dista del "create_time" por 5 minutos. Si se intenta tokenizar la tarjeta después de los 5 minutos, la tokenización fallará.

**Obtendrás los links:**

- **self**: desde esta URL puedes consultar la información de la intención de captura. [Ejemplo de ejecución de Self](self-capture.md).
- **capture_url**: desde esta se abre el iframe para que usuario complete los datos y tokenice su tarjeta.
- **capture**: desde esta se debe tokenizar/capturar tarjeta [Ejemplo de ejecución del capture/tokenización](json-capture.md).


> Estas URLs son dinamicas, nunca debes guardarlas como variables de entorno. Siempre debes consultarlas desde aquí para continuar con los pasos siguientes.

> **Si usas el capture_url** para que tus usuarios puedan tokenizar por iframe, debes recordar que tu modelo de integración sea el llamar al Api Single Sign ON (cuya vigencia del token generado por esta api tenga configurado un valor mayor o igual a los 10 minutos) e inmediatamente después llamar a la creación de intención de captura y del mismo modo, mostrar el iframe Quickpay Connect para tokenizar. Se recomienda crear el documento e inmediatamente mostrar el iframe con la url generada.
