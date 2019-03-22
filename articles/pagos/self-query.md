# ¿Cómo puedes revisar el estado de la consulta?

Debes llamar al self obtenido en la respuesta de la intención de consulta de la siguiente forma:

```
curl -X GET \
  https://api.qa.peinau.fif.tech/query/queries/{id} \
  -H 'authorization: access_token' \
 ```

Obtendrás una respuesta similar a:

```
{
    "_id": "5c94d8c3aebebc00168c6fa7",
    "query": "CMR_POINTS",
    "application": "5b76c4b1c06059001b6cad84",
    "links": [
        {
            "href": "https://api.qa.peinau.fif.tech/query/queries/5c94d8c3aebebc00168c6fa7",
            "rel": "self",
            "method": "GET",
            "security": []
        },
        {
            "href": "https://api.qa.peinau.fif.tech/query/queries/gateways/cmr/points/5c94d8c3aebebc00168c6fa7/query",
            "rel": "query_url",
            "method": "REDIRECT",
            "security": []
        }
    ],
    "redirect_urls": {
        "return_url": "https://google.com",
        "cancel_url": "https://outlook.live.com/owa/"
    },
    "customer": {
        "country": "CL",
        "name": "Jose Galvans",
        "document_type": "RUT",
        "document_number": "123451238",
        "is_guest": false
    },
    "expiration_time": "2019-03-22T12:47:51.108Z",
    "update_time": "2019-03-22T12:44:51.108Z",
    "create_time": "2019-03-22T12:44:51.108Z",
    "state": "created",
    "invoice_number": "QRY-1553258691108",
    "id": "5c94d8c3aebebc00168c6fa7"
}
```
> Esta información es identica a la respuesta obtenida en la respuesta de la intencion de consulta

# Ejemplo de Self incorrecto

Enviando un id incorrecto

```
curl -X GET \
  https://api.qa.peinau.fif.tech/query/queries/{id_incorrecto} \
  -H 'authorization: access_token' \
 ```

Obtendrás una respuesta similar a:

```
{
    "error_code": "DOCUMENT_NOT_FOUND",
    "error_description": "the document you requested is not found",
    "meta_data": {
        "id_not_found": "5c94d8c3aebebc00168c6fa8"
    },
    "statusCode": 404
}
```
