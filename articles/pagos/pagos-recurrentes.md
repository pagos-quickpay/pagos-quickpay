## Crear nueva intención de pago

Para ejecutar el pago recurrente debes crear una nueva intención de pago con el **token de la tarjeta (id)** obtenido previamente en el campo **capture_token**de la respuesta del pago original, el **access_token** generado en el [paso 1](obtener-token-acceso.md), y hacer el llamado de la siguiente forma:

> Para completar los datos del pago puedes utilizar la información enviada en la intención de pago original

```
curl -X POST \
  https://api.sandbox.connect.fif.tech/checkout/payments \
  -H 'authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJwcmltYXJ5c2lkIjoiMjhhZGI5OTktN2EyZS03MGI4LWMwOTItZTRjMTZhOWU5ZTBhIiwidW5pcXVlX25hbWUiOiJUb2lwYXRvLmNvbSIsImdyb3Vwc2lkIjoiQVBQTCIsImlzcyI6IkZhbGFiZWxsYSIsImF1ZCI6IldlYiIsInR5cGUiOiJCZWFyZXIiLCJzY29wZSI6W10sImlhdCI6MTUxMzE3Nzk1OCwiZXhwIjoxNTEzMTc4ODU4fQ.OYBksNEvNBU012fJt4IhUnQ5g0szPXPmivD2GvprLczjbG6Pd7HeSyWddSCVOAwAXfycNMzwn0nb_6VdYMqbSzE3T9Bu0Oqzih4b_BfLLb4EwpRQ3L0ObFNkJTI2hfIMUNJQ5ohT8b2yR-1SiehAUd0Tlkb3zrh2aDP9AYVZGqkjLdnwQOpBtXVs6VmntXnb3_MklOU7U0BylB1kVG40t9qfSxf79DYTcr3JWs6LdCFDThkudMZtJfnjYsOoqt--Iv8BzhCU7Eft1Isf2Qfqn_1-p778E7r4yQY1GREuAsXPNfnnHxi7gOVVQ1owq1aekqt4m4ML-VLow8pUx5duYw' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/json' \
  -H 'postman-token: fdd285bc-5f48-7c71-b306-19ee7d04941e' \
  -d '{ 
   "intent": "sale", 
   "payer": { 
     "payer_info": { 
       "email": "jlprueba1@quickpay.com", 
       "full_name": "Andres Roa",
       "country": "CL",
       "document_number": "123123123",
       "document_type": "RUT"
     }, 
     "payment_method": "QUICKPAY_TOKEN"
   }, 
   "transaction": { 
     "reference_id": "OD0000233", 
     "description": "Transaction detailed description", 
     "soft_descriptor": "Short Description", 
     "amount": { 
       "currency": "CLP", 
       "total": 4500, 
       "details": { 
         "subtotal": 810, 
         "tax": 190, 
         "shipping": 0, 
         "shipping_discount": 0 
       } 
     }, 
     "item_list": { 
       "shipping_address": { 
         "line1": "Miraflores 222", 
         "city": "Santiago", 
         "country_code": "CL", 
         "phone": "+56 9 1234 5674", 
         "type": "HOME_OR_WORK", 
         "recipient_name": "Andres Roa" 
       }, 
       "shipping_method": "DIGITAL", 
       "items": [ 
         { 
           "sku": "1231232", 
           "name": "Destornillador 2344", 
           "description": "Destornillador SCL - ONT", 
           "quantity": 1, 
           "price": 4500, 
           "tax": 0 
         } 
       ] 
     } 
   }, 
   "redirect_urls": { 
     "return_url": "https://peinau.azureedge.net/redirections/payment_success.html", 
     "cancel_url": "https://chao.com" 
   },
   "additional_attributes": {
   	"capture_token": "13b7c0f0-619b-ccf2-83e5-f33bcf2c4cd1"
  }
 }'
 ```
**Detalle de los Campos de la Petición**

| Nombre                                   | Descripción                              | Tipo         |
| ---------------------------------------- | ---------------------------------------- | ------------ |
| intent                                   | Identifica en tipo de transacción: Venta | string       |
| **payer**                                | **Pagador**                              | **object**   |
| **payer.payer_info**                     | **Información del cliente que está comprando en el sitio del  comercio** | **object**   |
| payer.payer_info.email                   | correo electrónico                       | string       |
| payer.payer_info.full_name               | nombre completo                          | string       |
| payer.payer_info.country                 | Nacionalidad                             | string       |
| payer.payer_info.document_number          | Número de identificación                 | string       |
| payer.payer_info.document_type            | Tipo de documento de identificación      | string       |
| payer.payment_method                     | Identifica el método de captura a utilizar (PEINAU_CAPTURE)  | string       |
| **transaction**                          | **Grupo de campos con la información de la transacción** | **object**   |
| transaction.gateway_order                | Número de la orden de compra. Id de transacción que es enviada al  gateway de pago. **Este valor debe ser unico** | string       |
| transaction.reference_id                 | El código de referencia de la transacción. Representa el identificador de  la transacción en el sistema del comercio. | string       |
| transaction.description                  | Descripción de la compra                 | string       |
| transaction.soft_descriptor              | Descripción corta de la transacción      | string       |
| **transaction.amount**                   | **Grupo de campos que detalla los montos de la compra** | **object**   |
| transaction.amount.currency              | Código ISO de la moneda asociada al monto de la compra. | string       |
| transaction.amount.total                 | Monto total de la compra que será descontado de la tarjeta o cuenta del  cliente | number          |
| transaction.amount.details               | Detalles del monto de la compra          |              |
| transaction.amount.details.subtotal      | Monto de la compra sin incluir impuesto  | number          |
| transaction.amount.details.tax           | Monto total de los impuestos             | number          |
| transaction.amount.details.shipping      | Costo del despacho                       | number          |
| transaction.amount.details.shipping_discount | Monto de descuento en costo de despacho  | number          |
| **transaction.item_list**                | **Información del producto(s)**         | **object**   |
| **transaction.item_list.shipping_address** | **Dirección de despacho (compras con despacho a domicilio)** | **object**   |
| transaction.item_list.shipping_address.line1 | Direccion de despaho                     | string       |
| transaction.item_list.shipping_address.city | Ciudad donde se realizará el despacho    | string       |
| transaction.item_list.shipping_address.country_code | Código de país donde se efectúa el despacho | string       |
| transaction.item_list.shipping_address.phone | Número de teléfono para la recepción de los productos despachados | string       |
| transaction.item_list.shipping_address.type | Tipo de despacho                         | string       |
| transaction.item_list.shipping_address.recipient_name | Nombre de la persona que recibirá el producto | string       |
| transaction.item_list.shipping_method    | Método de despacho de la compra: Digital, | string       |
| **transaction.item_list.items**          | **Grupo de campos que detalla los productos o servicios de la compra** | **objeto**   |
| transaction.item_list.items.sku          | Código SKU                               | string       |
| transaction.item_list.items.name         | Nombre del producto                      | string       |
| transaction.item_list.items.description  | Descripción del producto                 | string       |
| transaction.item_list.items.quantity     | Cantidad                                 | string       |
| transaction.item_list.items.price        | Precio unitario                          | number          |
| transaction.item_list.items.tax          | Monto del impuesto del producto          | number          |
| **redirect_urls**                        | **Url de redirección dependiendo del estado de la captura una vez  finalizado el proceso de captura** | **objeto**   |
| redirect_urls.return_url                 | URL de notificación de pago exitoso      | string (url) |
| redirect_urls.cancel_url                 | URL de notificación de pago fallido      | string (url) |
| **additional_attributes**                | **Grupo de campos de uso exclusivo**     | **objeto**   |
| additional_attributes.capture_token      | ID de captura de tarjeta                 | string       |
| additional_attributes.remember_capture | Marca para identificar si el cliente decide guardar la tarjeta | boolean      |

El resultado de la llamada a la API de checkout, será una nueva intención de pago en su estado inicial (created), que contendrá el, o los links HATEOAS relacionados con la llamada.

A continuación se presenta ejemplo de un JSON como respuesta al crear una intención de pago a través de la API RESTful de checkout:

```
{
    "intent": "sale",
    "additional_attributes": {
        "capture_token": "13b7c0f0-619b-ccf2-83e5-f33bcf2c4cd1"
    },
    "application": "28adb999-7a2e-70b8-c092-e4c16a9e9e0a",
    "redirect_urls": {
        "return_url": "https://peinau.azureedge.net/redirections/payment_success.html",
        "cancel_url": "https://chao.com"
    },
    "transaction": {
        "reference_id": "OD0000233",
        "description": "Transaction detailed description",
        "soft_descriptor": "Short Description",
        "item_list": {
            "shipping_method": "DIGITAL",
            "items": [
                {
                    "sku": "1231232",
                    "name": "Destornillador 2344",
                    "description": "Destornillador SCL - ONT",
                    "quantity": 1,
                    "price": 4500,
                    "tax": 0
                }
            ],
            "shipping_address": {
                "line1": "Miraflores 222",
                "city": "Santiago",
                "country_code": "CL",
                "phone": "+56 9 1234 5674",
                "type": "HOME_OR_WORK",
                "recipient_name": "Andres Roa"
            }
        },
        "amount": {
            "currency": "CLP",
            "total": 4500,
            "details": {
                "subtotal": 810,
                "tax": 190,
                "shipping": 0,
                "shipping_discount": 0
            }
        }
    },
    "payer": {
        "payer_info": {
            "document_type": "RUT",
            "document_number": "123123123",
            "country": "CL",
            "full_name": "Andres Roa",
            "email": "jlprueba1@quickpay.com"
        },
        "payment_method": "QUICKPAY_TOKEN"
    },
    "links": [
        {
            "href": "https://api.sandbox.connect.fif.tech/checkout/payments/aedac5dc-49a2-87db-e373-aa44675951a7",
            "rel": "self",
            "security": [
                "ApiKey"
            ],
            "method": "GET"
        },
        {
            "href": "https://api.sandbox.connect.fif.tech/checkout/payments/gateways/quickpay/token/aedac5dc-49a2-87db-e373-aa44675951a7/pay",
            "rel": "approval_url",
            "method": "REDIRECT"
        },
        {
            "href": "https://api.sandbox.connect.fif.tech/checkout/payments/aedac5dc-49a2-87db-e373-aa44675951a7/edit",
            "rel": "update_url",
            "method": "PUT"
        },
        {
            "href": "https://api.sandbox.connect.fif.tech/checkout/payments/gateways/quickpay/token/aedac5dc-49a2-87db-e373-aa44675951a7/silent",
            "rel": "silent_charge",
            "security": [
                "Jwt"
            ],
            "method": "POST"
        },
        {
            "href": "https://api.sandbox.connect.fif.tech/checkout/payments/gateways/quickpay/token/aedac5dc-49a2-87db-e373-aa44675951a7/refund",
            "rel": "refund_method",
            "security": [
                "Jwt"
            ],
            "method": "POST"
        }
    ],
    "id": "aedac5dc-49a2-87db-e373-aa44675951a7",
    "create_time": "2018-01-15T15:57:20.191Z",
    "update_time": "2018-01-15T15:57:20.191Z",
    "state": "created",
    "invoice_number": "INPA-50000001613"
}
```
**Detalle de los campos de la Respuesta**

| Nombre                                   | Descripción                              | Tipo         |
| ---------------------------------------- | ---------------------------------------- | ------------ |
| intent                                   | Identifica en tipo de transacción: Venta | string       |
| **payer**                                | **Pagador**                              | **object**   |
| **payer.payer_info**                     | **Información del cliente que está comprando en el sitio del  comercio** | **object**   |
| payer.payer_info.email                   | correo electrónico                       | string       |
| payer.payer_info.full_name               | nombre completo                          | string       |
| payer.payer_info.country                 | Nacionalidad                             | string       |
| payer.payer_info.document_number          | Número de identificación                 | string       |
| payer.payer_info.document_type            | Tipo de documento de identificación      | string       |
| payer.payment_method                     | Identifica el método de pago a utilizar  | string       |
| **transaction**                          | **Grupo de campos con la información de la transacción** | **object**   |
| transaction.gateway_order                | Número de la orden de compra. Id de transacción que es enviada al  gateway de pago. **Este valor debe ser unico** | string       |
| transaction.reference_id                 | El código de referencia de la transacción. Representa el identificador de  la transacción en el sistema del comercio. | string       |
| transaction.description                  | Descripción de la compra                 | string       |
| transaction.soft_descriptor              | Descripción corta de la transacción      | string       |
| **transaction.amount**                   | **Grupo de campos que detalla los montos de la compra** | **object**   |
| transaction.amount.currency              | Código ISO de la moneda asociada al monto de la compra. | string       |
| transaction.amount.total                 | Monto total de la compra que será descontado de la tarjeta o cuenta del  cliente | number          |
| transaction.amount.details               | Detalles del monto de la compra          |              |
| transaction.amount.details.subtotal      | Monto de la compra sin incluir impuesto  | number          |
| transaction.amount.details.tax           | Monto total de los impuestos             | number          |
| transaction.amount.details.shipping      | Costo del despacho                       | number          |
| transaction.amount.details.shipping_discount | Monto de descuento en costo de despacho  | number          |
| **transaction.item_list**                | **Información del producto(s)**         | **object**   |
| **transaction.item_list.shipping_address** | **Dirección de despacho (compras con despacho a domicilio)** | **object**   |
| transaction.item_list.shipping_address.line1 | Direccion de despaho                     | string       |
| transaction.item_list.shipping_address.city | Ciudad donde se realizará el despacho    | string       |
| transaction.item_list.shipping_address.country_code | Código de país donde se efectúa el despacho | string       |
| transaction.item_list.shipping_address.phone | Número de teléfono para la recepción de los productos despachados | string       |
| transaction.item_list.shipping_address.type | Tipo de despacho                         | string       |
| transaction.item_list.shipping_address.recipient_name | Nombre de la persona que recibirá el producto | string       |
| transaction.item_list.shipping_method    | Método de despacho de la compra: Digital, | string       |
| **transaction.item_list.items**          | **Grupo de campos que detalla los productos o servicios de la compra** | **objeto**   |
| transaction.item_list.items.sku          | Código SKU                               | string       |
| transaction.item_list.items.name         | Nombre del producto                      | string       |
| transaction.item_list.items.description  | Descripción del producto                 | string       |
| transaction.item_list.items.quantity     | Cantidad                                 | string       |
| transaction.item_list.items.price        | Precio unitario                          | number          |
| transaction.item_list.items.tax          | Monto del impuesto del producto          | number          |
| **redirect_urls**                        | **Url de redirección dependiendo del estado de la captura una vez  finalizado el proceso de captura** | **objeto**   |
| redirect_urls.return_url                 | URL de notificación de pago exitoso      | string (url) |
| redirect_urls.cancel_url                 | URL de notificación de pago fallido      | string (url) |
| **additional_attributes**                | **Grupo de campos de uso exclusivo**     | **objeto**   |
| additional_attributes.capture_token      | ID de captura de tarjeta                 | string       |
| additional_attributes.remember_capture | Marca para identificar si el cliente decide guardar la tarjeta | boolean|
| id                                       | Identificador unico de la intención      | string (Guid)|
| create_time                              | Fecha de creación de la intención        | string (ISO 8601)|
| update_time                              | Fecha de actualización de la intención   | string (ISO 8601)|
| invoice_number                           | Identificador legible de la intención    | string (correlativo)|
| application                           | Identificador interno    | string|
| links | Arreglo de Link HATEOAS para la ejecución de operaciones disponibles sobre la intención | array |
| **link** | Enlace bajo formato HATEOAS, sobre la definición de una operación disponible en una intención  | **objeto**  |
| link.href | Dirección URL de la operación | string (URL) |
| link.rel |Relación de la operación sobre una intención | Enum |
| link.method |Verbo HTTP solicitado para la ejecución de la operación|Enum|

**Detalle de las URLs generadas:**

- **self**: desde esta URL puedes consultar la información de la captura. [Ejemplo de ejecución de Self](self.md).
- **approval_url**: desde esta URL el cliente debe autorizar el pago.
- **update_url**: a partir de esta url podrás actualizar ciertos datos de la intención de pago.
- **silent_charge**: llamando a este endpoint desde la [API silent_charge] puedes ejecutar el cargo a la tarjeta de cŕedito del cliente sin pasar por la intención de pago.
- **refund_method**: para anular la transacción, debes hacer el llamado a este endpoint desde la [API de Anulación](anulacion.md).

> Estas URLs son dinamicas, nunca debes guardarlas como variables de entorno. Siempre debes consultarlas desde aquí para continuar con los pasos siguientes.

## Realizar el cargo a la tarjeta

Necesitas el **access_token** obtenido en la **Autenticación** y la **url silent charge** obtenida en el paso anterior para ejecutar una llamada a la **API de Silent Charge /silent** de la siguiente forma:

```
curl -v -X PUT 'https://api.sandbox.connect.fif.tech/checkout/payments/{id}/silent' \
  
 -H "Content-Type: application/json" \
 -H "Authorization: Bearer access_token"
 -d '{  
   	"installments_number": 1,
     }'
 
```

Obtendrás una respuesta en formato json. Dicha respuesta contendrá toda la información que previamente has enviado a la intención de pago y dependiendo del resultado del pago, se agrega lo siguiente:

Si el pago fue exitoso, verás el campo **state** con valor **paid** y un objeto llamado **gateway** que contiene la totalidad de información del pago exitoso. Esta información puede variar en formato dependiendo del gateway de pago utilizado. Dentro de **gateway**, verás el objeto llamado **resume**, el cual siempre tendrá la misma estructura y tus sistemas podrán utilizarlo siempre para obtener la información del pago.

Posibles estados de la transacción:

| State    | Definición                               |
| -------- | ---------------------------------------- |
| paid  | El cargo fue realizado exitosamente en la cuenta del cliente |
| rejected | Transacción fallida. El cargo no fue realizado |
| partially_refunded | Tiene al menos una devolución asociada |


**Pago exitoso**
Descripción de los campos que deben utilizar tus sistemas para obtener la respuesta del pago

| Nombre    | Descripción                               |Tipo|
| -------- | ---------------------------------------- |-------|
| state  | Identifica el estado del pago |enum|
| gateway  | Identifica el grupo de campos con la información detallada del pago exitoso |object|
| gateway.resume | resumen de la información del pago exitoso |object|
| gateway.resume.id | Identificador interno de la aplicación |string|
| gateway.resume.card_number | datos del PAN truncado |object|
| gateway.resume.card_number.pan_last4 | Últimos 4 dígitos del PAN |number|
| gateway.resume.card_number.pan_first6 | Primeros 6 dígitos del PAN |number|
| gateway.resume.authorizations | Información del código de autorización |object|
| gateway.resume.authorizations.code | Código de autorización |string|
| gateway.resume.transaction | Datos de la transacción |object|
| gateway.resume.transaction.gateway_id | Identificador interno de la aplicación |string|
| gateway.resume.transaction.type | Tipo de transacción |enum (CREDIT / DEBIT)|
| gateway.resume.transaction.date | Fecha y hora de registro de transacción en el gateway |string|
| gateway.resume.transaction.currency | Tipo moneda |string|
| gateway.resume.transaction.buy_order | Número de la orden de compra que el comercio envio en el campo **transaction.gateway_order** de la intención de pago |string|
| gateway.resume.transaction.amount | Monto total de la compra que el comercio envió en el campo **transaction.amount.total** de la intención de pago |number|
| gateway.resume.transaction.installments_number | Número de cuotas que el comercio envió en el campo **installments_number** del silent charge |number|
| gateway.resume.response | Infromación del código de respuesta entregado por el gateway |object|
| gateway.resume.response.code | Código de respuesta entregado por el gateway |number|

Ejemplo de respuesta Silent charge (Json completo): 

```
{
    "intent": "sale",
    "additional_attributes": {
        "capture_token": "13b7c0f0-619b-ccf2-83e5-f33bcf2c4cd1"
    },
    "application": "28adb999-7a2e-70b8-c092-e4c16a9e9e0a",
    "redirect_urls": {
        "return_url": "https://peinau.azureedge.net/redirections/payment_success.html",
        "cancel_url": "https://chao.com"
    },
    "transaction": {
        "reference_id": "OD0000233",
        "description": "Transaction detailed description",
        "soft_descriptor": "Short Description",
        "item_list": {
            "shipping_method": "DIGITAL",
            "items": [
                {
                    "sku": "1231232",
                    "name": "Destornillador 2344",
                    "description": "Destornillador SCL - ONT",
                    "quantity": 1,
                    "price": 4500,
                    "tax": 0,
                    "_id": "5a5ccf5f79c83f0014632599"
                }
            ],
            "shipping_address": {
                "line1": "Miraflores 222",
                "city": "Santiago",
                "country_code": "CL",
                "phone": "+56 9 1234 5674",
                "type": "HOME_OR_WORK",
                "recipient_name": "Andres Roa"
            }
        },
        "amount": {
            "currency": "CLP",
            "total": 4500,
            "details": {
                "subtotal": 810,
                "tax": 190,
                "shipping": 0,
                "shipping_discount": 0
            }
        }
    },
    "payer": {
        "payer_info": {
            "document_type": "RUT",
            "document_number": "123123123",
            "country": "CL",
            "full_name": "Andres Roa",
            "email": "jlprueba1@quickpay.com"
        },
        "payment_method": "QUICKPAY_TOKEN"
    },
    "links": [],
    "id": "aedac5dc-49a2-87db-e373-aa44675951a7",
    "create_time": "2018-01-15T15:57:20.191Z",
    "update_time": "2018-01-15T15:57:42.622Z",
    "state": "paid",
    "invoice_number": "INPA-50000001613",
    "gateway": {
        "installments_number": 36,
        "merchantReferenceCode": "INPA-50000001613",
        "requestID": "5160318622226245704012",
        "decision": "ACCEPT",
        "reasonCode": "100",
        "requestToken": "Ahj//wSTF73Ojl/8i1lMiiDBlYjWmciPKhWY82VamJcW4Q6B4ClxbhDoHkwNjKPp8MmkmXoxXL8sBgTkxe9zo5f/ItZTAAAA+hPE",
        "purchaseTotals": {
            "currency": "CLP"
        },
        "ccAuthReply": {
            "reasonCode": "100",
            "amount": "4500",
            "authorizationCode": "570110",
            "avsCode": "1",
            "authorizedDateTime": "2018-01-15T15:57:42Z",
            "processorResponse": "1",
            "reconciliationID": "02XFZ3HGJBYGMJZL",
            "paymentNetworkTransactionID": "111222",
            "ownerMerchantID": "falabella2",
            "processorTransactionID": "152e471b288543c89e2f33d2fe0ac722"
        },
        "ccCaptureReply": {
            "reasonCode": "100",
            "requestDateTime": "2018-01-15T15:57:42Z",
            "amount": "4500",
            "reconciliationID": "02XFZ3HGJBYGMJZL"
        },
        "additionalProcessorResponse": "2fd6e9c9-4280-4134-a0a2-a67ee8f79a3c",
        "capture_token": "13b7c0f0-619b-ccf2-83e5-f33bcf2c4cd1",
        "resume": {
            "_id": "5a5ccf76b35dd40014db701a",
            "card_number": {
                "pan_last4": 1111,
                "pan_first6": 411111
            },
            "authorizations": {
                "code": "570110"
            },
            "transaction": {
                "gateway_id": "5160318622226245704012",
                "type": "CREDIT",
                "date": "2018-01-15T15:57:42.622Z",
                "currency": "CLP",
                "buy_order": "INPA-50000001613",
                "amount": 4500,
                "installments_number": 1
            },
            "response": {
                "code": 100
            }
        }
    }
}
```

[Ejemplo de silent charge fallido](transaccion-fallida.md)

Además, agregamos información específica del código entregado por el Gateway CyberSource (Estructura resume del JSON de respuesta). [Ver la lista de códigos de respuesta CyberSource aquí](cybersource_reason_code.md).

[Consultar estado del servicio (Health Check)](health-checkout.md)



