## 2. Intención de Pago

Para generar una intención de pago debes hacer una petición a la API de **Intención de Pago /payments** con el **access_token** generado en el [paso 1](obtener-token-acceso.md)

**Ejemplo:**
```
curl -X POST \
  https://api.sandbox.connect.fif.tech/checkout/payments \
  -H 'authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJwcmltYXJ5c2lkIjoiMjhhZGI5OTktN2EyZS03MGI4LWMwOTItZTRjMTZhOWU5ZTBhIiwidW5pcXVlX25hbWUiOiJUb2lwYXRvLmNvbSIsImdyb3Vwc2lkIjoiQVBQTCIsImlzcyI6IkZhbGFiZWxsYSIsImF1ZCI6IldlYiIsInR5cGUiOiJCZWFyZXIiLCJzY29wZSI6W10sImlhdCI6MTUxMzE3Nzk1OCwiZXhwIjoxNTEzMTc4ODU4fQ.OYBksNEvNBU012fJt4IhUnQ5g0szPXPmivD2GvprLczjbG6Pd7HeSyWddSCVOAwAXfycNMzwn0nb_6VdYMqbSzE3T9Bu0Oqzih4b_BfLLb4EwpRQ3L0ObFNkJTI2hfIMUNJQ5ohT8b2yR-1SiehAUd0Tlkb3zrh2aDP9AYVZGqkjLdnwQOpBtXVs6VmntXnb3_MklOU7U0BylB1kVG40t9qfSxf79DYTcr3JWs6LdCFDThkudMZtJfnjYsOoqt--Iv8BzhCU7Eft1Isf2Qfqn_1-p778E7r4yQY1GREuAsXPNfnnHxi7gOVVQ1owq1aekqt4m4ML-VLow8pUx5duYw' \
  -H 'content-type: application/json' \
  -d '{
  "intent": "sale",
  "payer": {
    "payer_info": {
      "email": "aroa@gmail.com",
      "full_name": "Andres Roa",
      "country": "CL",
      "document_number": "371119582",
      "document_type": "RUT"
    },
    "payment_method": "PAGOINAPP_CREDIT"
  },
  "transaction": {
    "description": "Compra COPEC Chesterton",
    "soft_descriptor": "COPEC-PAGO-CLICK",
    "item_list": {
      "shipping_method": "DIGITAL",
      "items": [
        {
          "thumbnail": "http://portal.test.peinau.fif.tech/bundles/app/css/images/e-commerce-demo/product-icon.png",
          "sku": "GASOLINA",
          "name": "Gas. 93",
          "description": "Gasolina 93, 45lts",
          "quantity": 1,
          "price": 30000,
          "tax": 0,
          "_id": "5a7a14343df88b000fdac92a"
        },
        {
          "thumbnail": "http://portal.test.peinau.fif.tech/bundles/app/css/images/e-commerce-demo/product-icon.png",
          "sku": "DESCLIP",
          "name": "Desc Socio",
          "description": "Descuento Socio",
          "quantity": 1,
          "price": -1500,
          "tax": 0,
          "_id": "5a7a14343df88b000fdac929"
        },
        {
          "thumbnail": "http://portal.test.peinau.fif.tech/bundles/app/css/images/e-commerce-demo/product-icon.png",
          "sku": "DESGASO93",
          "name": "Desc Falabella",
          "description": "Destalle Descuento Falabella",
          "quantity": 1,
          "price": -2000,
          "tax": 0,
          "_id": "5a7a14343df88b000fdac928"
        }
      ],
      "shipping_address": {
        "line1": "Dirección Sucursal Matriz Copec",
        "city": "Santiago",
        "country_code": "CL",
        "phone": "+56 9 8762 1244",
        "type": "HOME_OR_WORK",
        "recipient_name": "Jhon Doe Son"
      }
    },
    "amount": {
      "currency": "CLP",
      "total": 26500,
      "details": {
        "subtotal": 26500,
        "tax": 0,
        "shipping": 0,
        "shipping_discount": 0
      }
    }
  },
  "redirect_urls": {
    "return_url": "http://portal.sandbox.connect.fif.tech",
    "cancel_url": "http://portal.sandbox.connect.fif.tech"
  },
  "additional_attributes": {
  }
}'
 ```
> Tienes los siguientes metodos de pago disponibles:
> **"payment_method": "PAGOINAPP_CREDIT"** Pagos en la App CMR
> **"payment_method": "PAGOINAPP_DEBIIT"** Pagos en la App Banco Falabella
> **"payment_method": "CARDBILL_PAYMENT_DEBIT_BF"** Pagos de estado de cuenta de Tarjeta CMR en App CMR

**Detalle de los Campos de la Petición**

| Nombre                                   | Descripción                              | Tipo         |
| ---------------------------------------- | ---------------------------------------- | ------------ |
| intent                                   | Identifica en tipo de transacción: Venta | string       |
| **payer**                                | **Pagador**                              | **object**   |
| **payer.payer_info**                     | **Información del cliente que está comprando en el sitio del  comercio** | **object**   |
| payer.payer_info.email                   | correo electrónico                       | string       |
| payer.payer_info.full_name               | nombre completo                          | string       |
| payer.payer_info.country                 | Nacionalidad                             | string       |
| payer.payer_info.documentNumber          | Número de identificación                 | string       |
| payer.payer_info.documentType            | Tipo de documento de identificación      | string       |
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

El resultado de la llamada a la API de checkout, será una intención de pago en su estado inicial (created), que contendrá el, o los links HATEOAS relacionados con la llamada.

A continuación se presenta ejemplo de un JSON como respuesta al crear una intención de pago a través de la API RESTful de checkout:

```
{
    "application": "5af0799cd1aa8e000f9de4ca",
    "_id": "5b6121d4d28fc400163111d6",
    "redirect_urls": {
        "return_url": "http://portal.sandbox.connect.fif.tech",
        "cancel_url": "http://portal.sandbox.connect.fif.tech"
    },
    "transaction": {
        "gateway_order": "INPA-1533092308183",
        "description": "Compra COPEC Chesterton",
        "soft_descriptor": "COPEC-PAGO-CLICK",
        "item_list": {
            "shipping_method": "DIGITAL",
            "items": [
                {
                    "thumbnail": "http://portal.test.peinau.fif.tech/bundles/app/css/images/e-commerce-demo/product-icon.png",
                    "sku": "GASOLINA",
                    "name": "Gas. 93",
                    "description": "Gasolina 93, 45lts",
                    "quantity": 1,
                    "price": 30000,
                    "tax": 0,
                    "_id": "5a7a14343df88b000fdac92a"
                },
                {
                    "thumbnail": "http://portal.test.peinau.fif.tech/bundles/app/css/images/e-commerce-demo/product-icon.png",
                    "sku": "DESCLIP",
                    "name": "Desc Socio",
                    "description": "Descuento Socio",
                    "quantity": 1,
                    "price": -1500,
                    "tax": 0,
                    "_id": "5a7a14343df88b000fdac929"
                },
                {
                    "thumbnail": "http://portal.test.peinau.fif.tech/bundles/app/css/images/e-commerce-demo/product-icon.png",
                    "sku": "DESGASO93",
                    "name": "Desc Falabella",
                    "description": "Destalle Descuento Falabella",
                    "quantity": 1,
                    "price": -2000,
                    "tax": 0,
                    "_id": "5a7a14343df88b000fdac928"
                }
            ],
            "shipping_address": {
                "line1": "Dirección Sucursal Matriz Copec",
                "city": "Santiago",
                "country_code": "CL",
                "phone": "+56 9 8762 1244",
                "type": "HOME_OR_WORK",
                "recipient_name": "Jhon Doe Son"
            }
        },
        "amount": {
            "currency": "CLP",
            "total": 26500,
            "details": {
                "subtotal": 26500,
                "tax": 0,
                "shipping": 0,
                "shipping_discount": 0
            }
        }
    },
    "payer": {
        "payer_info": {
            "document_type": "RUT",
            "document_number": "371119582",
            "country": "CL",
            "full_name": "Andres Roa",
            "email": "aroa@gmail.com"
        },
        "payment_method": "PAGOINAPP_CREDIT"
    },
    "links": [
        {
            "href": "https://api.sandbox.connect.fif.tech/checkout/payments/5b6121d4d28fc400163111d6",
            "rel": "self",
            "method": "GET"
        },
        {
            "href": "https://api.sandbox.connect.fif.tech/checkout/payments/gateways/pagoinapp/credit/5b6121d4d28fc400163111d6/pay",
            "rel": "approval_url",
            "method": "REDIRECT"
        },
        {
            "href": "https://api.sandbox.connect.fif.tech/checkout/payments/5b6121d4d28fc400163111d6/edit",
            "rel": "update_url",
            "method": "PUT"
        },
        {
            "href": "https://api.sandbox.connect.fif.tech/checkout/payments/INPA-1533092308183",
            "rel": "self_by_gateway_order",
            "method": "GET"
        }
    ],
    "update_time": "2018-08-01T02:58:28.183Z",
    "create_time": "2018-08-01T02:58:28.183Z",
    "invoice_number": "INPA-1533092308183",
    "state": "created",
    "intent": "sale",
    "id": "5b6121d4d28fc400163111d6"
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
| payer.payer_info.documentNumber          | Número de identificación                 | string       |
| payer.payer_info.documentType            | Tipo de documento de identificación      | string       |
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

- **self**: desde esta URL puedes consultar la información de la intención de pago. [Ejemplo de ejecución de Self](self.md).
- **approval_url**: desde esta URL el cliente debe autorizar el pago.
- **update_url**: a partir de esta url podrás actualizar ciertos datos de la intención de pago.
- **self_by_gateway_order**: desde esta URL puedes consultar la información de la intención de pago.

> Estas URLs son dinamicas, nunca debes guardarlas como variables de entorno. Siempre debes consultarlas desde aquí para continuar con los pasos siguientes.

[Consultar estado del servicio (Health Check)](health-checkout.md)

Ir al paso [xxx](xxx.md)
