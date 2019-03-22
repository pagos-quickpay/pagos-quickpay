## Intención de Consulta

Para generar una intención de consulta debes hacer una petición a la API de **Intención de Consulta /queries** con el **access_token** generado en el [paso 1](obtener-token-acceso.md) y el JSON correspondiente al metodo de consulta (query) que quieras emplear.

- Consulta CMR Points [Json ejemplo query": "CMR_POINTS" ](json-consulta-cmr-points.md)

**Detalle de los Campos de la Petición**

| Nombre                                   | Descripción                              | Tipo         |    Requerido |
| ---------------------------------------- | ---------------------------------------- | ------------ | ------------ |
| query                                    | Identifica el tipo de consulta           | string       | Si           |
| **customer**                             | **Titular**                              | **object**   |              |
| customer.reference_id                    | El código de referencia de la consulta. Representa el identificador de  la consulta en el sistema del comercio. | string       | No       |
| customer.country                         | Nacionalidad                             | string       | Si           |
| customer.name                            | Nombre del cliente                       | string       | Si           |
| customer.email                           | correo electrónico                       | string       | Si           |
| customer.document_type                   | Tipo de documento de identificación      | string       | Si           |
| customer.document_number                 | Número de identificación                 | string       | Si           |
| customer.is_guest                        | Indica si es un cliente invitado o un cliente que hizo login en el comercio | string  | No       |
| **redirect_urls**                        | **Url de redirección dependiendo del estado de la consulta una vez finalizado el proceso de consulta** | **objeto**   |
| redirect_urls.return_url                 | URL de notificación de consulta exitoso  | string (url) | Si       |
| redirect_urls.cancel_url                 | URL de notificación de consulta fallida  | string (url) | Si       |

El resultado de la llamada a la API de query, será una intención de consulta en su estado inicial (created), que contendrá el, o los links HATEOAS relacionados con la llamada.

**Detalle de los campos de la Respuesta**

| Nombre                                   | Descripción                              | Tipo         |
| ---------------------------------------- | ---------------------------------------- | ------------ |
|                                    |  | string       |
