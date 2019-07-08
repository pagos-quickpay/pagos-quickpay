En ocasiones, querrás consultar los puntos de tu cliente sin la necesidad de que él interactue con un iframe para consultar para poder saber qué productos ofrecerle. En ese caso, te recomendamos utilizar la consulta silenciosa (no necesitarás crear una intención de consulta).

## Intención de Consulta

Para generar una intención de consulta debes hacer una petición a la API de **Intención de Consulta /queries** con el **access_token** generado en el [paso 1](obtener-token-acceso.md) y el JSON correspondiente al metodo de consulta (query) que quieras emplear.

- Consulta CMR Points [Json ejemplo query": "CMR_POINTS" ](json-consulta-cmr-points.md)

**Detalle de los Campos de la Petición**

| Nombre                                   | Descripción                              | Tipo         |    Requerido |
| ---------------------------------------- | ---------------------------------------- | ------------ | ------------ |
| query                                    | Identifica el tipo de consulta           | string       | Si           |
| **customer**                             | **Cliente**                              | **object**   |              |
| customer.country                         | Nacionalidad                             | string       | Si           |
| customer.name                            | Nombre del cliente                       | string       | Si           |
| customer.document_type                   | Tipo de documento de identificación      | string       | Si           |
| customer.document_number                 | Número de identificación                 | string       | Si           |
| customer.is_guest                        | Indica si es un cliente invitado o un cliente que hizo login en el comercio | string  | No       |
| **redirect_urls**                        | **Url de redirección dependiendo del estado de la consulta una vez finalizado el proceso de consulta** | **objeto**   |
| redirect_urls.return_url                 | URL de notificación de consulta exitoso  | string (url) | Si       |
| redirect_urls.cancel_url                 | URL de notificación de consulta fallida  | string (url) | Si       |

El resultado de la llamada a la API de query, será una intención de consulta en su estado inicial (created), que contendrá el, o los links HATEOAS relacionados con la llamada.

**Detalle de las URLs generadas:**

- **self**: desde esta URL puedes consultar la información de la intención de consulta. [Ejemplo de ejecución de Self](self-query.md).
- **query_url**: desde esta URL el cliente debe ejcutar la consulta de CMR Points. Esta desplegará el iframe de consulta y guardará la cantidad de punto en el documento de consulta si el usuario se loguea correctamente, o el parametro guest es igual a false (o sea, el comercio confía en el usuario). Al documento de consulta se puede acceder con el self.

> Estas URLs son dinamicas, nunca debes guardarlas como variables de entorno. Siempre debes consultarlas desde aquí para continuar con los pasos siguientes.

[Consultar estado del servicio (Health Check)](health-query.md)
