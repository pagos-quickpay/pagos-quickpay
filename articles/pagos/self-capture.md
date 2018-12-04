# ¿Cómo puedes consultar el estado de la transacción?

Debes llamar al self obtenido en la respuesta de la intención de pago de la siguiente forma:

```
curl -X GET \
  https://api.qa.peinau.fif.tech/tokenization/captures/{id} \
  -H 'authorization: access_token' \
 ```

Obtendrás una respuesta similar a:

```
{
    "_id": "bf7bcccf-7fef-461d-802a-0bc5ed4c7d23",
    "capture": "CMR_CAPTURE",
    "capture_method": "TOKENIZATION",
    "application": "5af350553dbed900146c5945",
    "additional_attributes": {
        "remember_capture": false
    },
    "gateway": {
        "status": "S",
        "category": "|||",
        "qpCardId": "1111484106953975",
        "panFirst6": "445596",
        "panLast4": "1434"
    },
    "links": [
        {
            "href": "http://localhost:8090/captures/bf7bcccf-7fef-461d-802a-0bc5ed4c7d23",
            "rel": "self",
            "method": "GET",
            "security": []
        },
        {
            "href": "http://localhost:8090/captures/gateways/cmr/capture/bf7bcccf-7fef-461d-802a-0bc5ed4c7d23/capture",
            "rel": "capture_url",
            "method": "REDIRECT",
            "security": []
        },
        {
            "href": "http://localhost:8090/captures/gateways/cmr/capture/bf7bcccf-7fef-461d-802a-0bc5ed4c7d23/capture",
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
        "name": "Alejandro Rivero",
        "email": "JLPrueba1@gmail.com"
    },
    "deletion_time": "2018-12-05T13:29:53.486Z",
    "update_time": "2018-12-04T13:30:08.146Z",
    "create_time": "2018-12-04T13:29:53.486Z",
    "state": "captured",
    "invoice_number": "INCA-1543930193486",
    "id": "bf7bcccf-7fef-461d-802a-0bc5ed4c7d23"
}
```
> Esta información es identica a la respuesta obtenida en la respuesta de la intencion de captura

# Ejemplo de Self incorrecto

Enviando un id incorrecto

```
curl -X GET \
  https://api.test.peinau.fif.tech/tokenization/captures/{id_incorrecto} \
  -H 'authorization: access_token' \
 ```

La respuesta obtenida es: 
* Status http **500**
* Glosa: **"DOCUMENT_NOT_FOUND"**
