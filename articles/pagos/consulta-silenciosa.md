Si deseas consultar los puntos de tu cliente (para saber qué productos ofrecerle) sin la necesidad de que él interactue con un iframe, te recomendamos utilizar la consulta silenciosa.

## Consulta silenciosa de puntos

Para realizar una consulta silenciosa, la debes hacer con el **access_token** (enviándolo como header) generado en el [paso 1](obtener-token-acceso.md) y enviar los parámetros requeridos en la url. A continuación, un ejemplo:

```
curl -X GET \
  'https://api.qa.peinau.fif.tech/query/queries/gateways/cmr/points/silent?country=CL&document_type=RUT&document_number=123456789' \
  -H 'Authorization: Bearer $ACCESS_TOKEN' \
  -H 'Cache-Control: no-cache' \
  -H 'Content-Type: application/json'
```
**Detalle de los parámetros de la Petición**

| Nombre                                   |    Requerido |
| ---------------------------------------- | ------------ |
| country                                  | Sí           |
| document_type                            | Sí           |
| document_number (debe enviarse sin puntos ni guiones) | Sí           |

Obtendrás el siguiente resultado en formato JSON:
```
{
    "kindOfPoints": "CMR_PUNTOS",
    "amountOfPoints": 2460,
    "pointsToExpire": 0,
    "dateToExpire": "2019-07-31"
}
```

[Regresar](introduction.md)
