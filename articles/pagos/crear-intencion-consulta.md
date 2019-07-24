Si deseas mostrar nuestro iframe de consulta de puntos CMR en tu sitio, necesitas crear una **intención de consulta**.

## Intención de Consulta

Para generar una intención de consulta debes hacer una petición a la API de **Intención de Consulta /queries** con el **access_token** generado en el [paso 1](obtener-token-acceso.md) y el JSON correspondiente al metodo de consulta (query) que quieras emplear.

- Consulta CMR Points [Json ejemplo query": "CMR_POINTS" ](json-consulta-cmr-points.md)

**Detalle de los Campos de la Petición**

| Nombre                                   | Descripción                              | Tipo         |    Requerido |
| ---------------------------------------- | ---------------------------------------- | ------------ | ------------ |
| query                                    | Identifica el tipo de consulta           | string       | Si           |
| **customer**                             | **Cliente**                              | **object**   |              |
| customer.country                         | Nacionalidad                             | string       | Si           |
| customer.name                            | Nombre del cliente                       | string       | No           |
| customer.document_type                   | Tipo de documento de identificación      | string       | Si           |
| customer.document_number                 | Número de identificación                 | string       | *            |
| customer.is_guest                        | Indica si es un cliente invitado o un cliente que hizo login en el comercio | Boolean  | Sí       |
| **redirect_urls**                        | **Url de redirección dependiendo del estado de la consulta una vez finalizado el proceso de consulta** | **objeto**   |
| redirect_urls.return_url                 | URL de notificación de consulta exitoso  | string (url) | No       |
| redirect_urls.cancel_url                 | URL de notificación de consulta fallida  | string (url) | No       |

**Importante**
El número de documento va a ser requerido de acuerdo al campo is_guest bajo el siguiente criterio:

| **is_guest**                         | **document_number**             | **Acción Quickpay**                       |
| ------------------------------------ | ------------------------------- | ----------------------------------------- |
| true                                 | Viene el Rut (RUT opcional)     | Se pide multiclave y se muestra rut por defecto, se permite cambio de rut|
| false                                | No viene el RUT (RUT requerido) | Se muestran los puntos directamente       |
| true                                 | No viene el RUT (RUT opcional)  | Se pide multiclave y rut, se permite cambio de rut|
| false                                | No viene el RUT (RUT requerido) | Se retorna error por campo requerido      |


El resultado de la llamada a la API de query, será una intención de consulta en su estado inicial (created), que contendrá el, o los links HATEOAS relacionados con la llamada.

**Detalle de los campos de la Respuesta**

| Nombre                                   | Descripción                              | Tipo         |
| ---------------------------------------- | ---------------------------------------- | ------------ |
| query                                    | Identifica el tipo de consulta           | string       |
| application                              | Identificador interno                    | string       |
| links                                    | Arreglo de Link HATEOAS para la ejecución de operaciones disponibles sobre la intención | array |
| **link**                                 | Enlace bajo formato HATEOAS, sobre la definición de una operación disponible en una intención  | **objeto**  |
| link.href                                | Dirección URL de la operación            | string (URL) |
| link.rel                                 |Relación de la operación sobre una intención | Enum |
| link.method                              |Verbo HTTP solicitado para la ejecución de la operación|Enum|
| **redirect_urls**                        | **Url de redirección dependiendo del estado de la consulta una vez  finalizado el proceso de consulta** | **objeto**   |
| redirect_urls.return_url                 | URL de notificación de consulta exitoso  | string (url) |
| redirect_urls.cancel_url                 | URL de notificación de consulta fallido  | string (url) |
| **customer**                             | **Cliente**                              | **object**   |
| customer.country                         | Nacionalidad                             | string       |
| customer.name                            | Nombre del cliente                       | string       |
| customer.document_type                   | Tipo de documento de identificación      | string       |
| customer.document_number                 | Número de identificación                 | string       |
| customer.is_guest                        | Indica si es un cliente invitado o un cliente que hizo login en el comercio |
| expiration_time                          | Fecha en la cual expiran los CMR Points  | string (ISO 8601)|
| update_time                              | Fecha de actualización de la intención   | string (ISO 8601)|
| create_time                              | Fecha de creación de la intención        | string (ISO 8601)|
| state                                    | Estado de la intención                   | string       |
| invoice_number                           | Identificador legible de la intención    | string (correlativo)|
| id                                       | Identificador unico de la intención      | string (Guid)|

**Detalle de las URLs generadas:**

- **self**: desde esta URL puedes consultar la información de la intención de consulta. [Ejemplo de ejecución de Self](self-query.md).
- **query_url**: desde esta URL el cliente debe ejcutar la consulta de CMR Points. Esta desplegará el iframe de consulta y guardará la cantidad de punto en el documento de consulta si el usuario se loguea correctamente, o el parametro guest es igual a false (o sea, el comercio confía en el usuario). Al documento de consulta se puede acceder con el self.

> Estas URLs son dinamicas, nunca debes guardarlas como variables de entorno. Siempre debes consultarlas desde aquí para continuar con los pasos siguientes.

[Consultar estado del servicio (Health Check)](health-query.md)
