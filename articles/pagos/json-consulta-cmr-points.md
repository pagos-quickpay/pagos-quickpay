## Ejemplo petición query": "CMR-POINTS"

```
curl -X POST \
  https://api.qa.peinau.fif.tech/query/queries \
  -H 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJwcmltYXJ5c2lkIjoiNWI3NmM0YjFjMDYwNTkwMDFiNmNhZDg0IiwidW5pcXVlX25hbWUiOiJCQ08gQ2hpbGUiLCJncm91cHNpZCI6IkFQUEwiLCJpc3MiOiJGYWxhYmVsbGEiLCJhdWQiOiJXZWIiLCJ0eXBlIjoiQmVhcmVyIiwic2NvcGUiOltdLCJpYXQiOjE1NTMyNTg2NDAsImV4cCI6MTU1MzI1OTI0MH0.b2LT2WZjvICYWiJD8kAGRwqqbDwivf_VSP1DBy096D7kj2A1kj2EcnYmqrgfq6sO4sIQQqYmUaffNzZKc8upY9xVaKJRFdXnS6pdv9ius1AS-h5jnIofdsUFPPr4g4PHv_q-wLYkvdQzwKkefuUPX3HfeiCzmlsZHYGXPlyZivkk67d4IlNeTJzkNdg0af2LtY88t4BK-f4mfZU0Z5ducjKQkNrUP7WGmY-b9xtIwaN2eSDqHsH4TaDh_RxRdHhO2ZnDwGk1SojRiBiqRshGLtdNV2xxBMpsJ1AixsE95TxEcHhyW78yo1qzt3eiQkP-eKedpmYNRI9W0wJ9yLm54A' \
  -H 'Cache-Control: no-cache' \
  -H 'Content-Type: application/json' \
  -H 'Postman-Token: 39ba4b7f-d051-451f-b16b-3a600f5a1507' \
  -d '{
 "query": "CMR_POINTS",
 "customer": {
   "reference_id": "001389",
   "country": "CL",
   "name": "Jose Galvans",
   "email": "JLPrueba1@gmail.com",
   "document_type": "RUT",
   "document_number": "123451238",
   "is_guest": "false"
 },
"redirect_urls": {
   "return_url": "https://google.com",
   "cancel_url": "https://outlook.live.com/owa/"
 }
}'
```

A continuación se presenta ejemplo de un JSON de respuesta obtenido al crear una intención de consulta a través de la API RESTful de query:

```
{
    "query": "CMR_POINTS",
    "application": "5b76c4b1c06059001b6cad84",
    "_id": "5c94d8c3aebebc00168c6fa7",
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

Posibles resultados de la transacción
