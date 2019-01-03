## 2. Intención de Pago

Para generar una intención de pago debes hacer una petición a la API de **Intención de Pago /payments** con el **access_token** generado en el [paso 1](obtener-token-acceso.md) y el JSON correspondiente al metodo de pago que quieras emplear.

- Pago in App Credit (APP CMR) [Json ejemplo payment_method": "PAGOINAPP_CREDIT" ](json-pago-credit.md)

- Pago in App Debit (APP Banco Falabella) [Json ejemplo payment_method": "PAGOINAPP_DEBIT" ](json-pago-debit.md)

- Pago de estado de cuenta de CMR con Cuenta de Banco Falabella [Json ejemplo payment_method": "CARDBILL_PAYMENT_DEBIT_BF" ](json-cardbill.md)

- Pago con CMR [Json ejemplo payment_method": "QUICKPAY_CREDIT" ](json-quickpay-credit.md)

- Pago con CMR con captura/tokenización previa [Json ejemplo payment_method": "QUICKPAY_CREDIT" ](json-captured-quickpay-credit.md)

- Pago con Debito de Banco Falabella [Json ejemplo payment_method": "QUICKPAY_DEBIT" ](json-quickpay-debit.md)

- Pago con CMR Credit Doc Id [Json ejemplo payment_method": "QUICKPAY_CREDIT_DOC_ID" ](json-quickpay-credit-doc-id.md)

- Pago con Tarjeta de Crédito de Terceros [Json ejemplo payment_method": "QUICKPAY_TOKEN" ](json-quickpay-token.md)

- Pago con Transbank Webpay [Json ejemplo payment_method": "TRANSBANK_WEBPAY" ](json-transbank-webpay.md)

**Detalle de los Campos de la Petición**

| Nombre                                   | Descripción                              | Tipo         |    Requerido |
| ---------------------------------------- | ---------------------------------------- | ------------ | ------------ |
| intent                                   | Identifica en tipo de transacción: Venta | string       | Si           |
| **payer**                                | **Pagador**                              | **object**   |         |
| **payer.payer_info**                     | **Información del cliente que está comprando en el sitio del  comercio** | **object**   |
| payer.payer_info.email                   | correo electrónico                       | string       | Si       |
| payer.payer_info.full_name               | nombre completo                          | string       | Si       |
| payer.payer_info.country                 | Nacionalidad                             | string       | Si       |
| payer.payer_info.document_number         | Número de identificación                 | string       | Si       |
| payer.payer_info.document_type           | Tipo de documento de identificación      | string       | Si       |
| payer.payer_info.is_guest                | Indica si es un cliente invitado o un cliente que hizo login en el comercio | string  | No       |
| payer.payment_method                     | Identifica el método de captura a utilizar (PEINAU_CAPTURE)  | string       | Si       |
| **transaction**                          | **Grupo de campos con la información de la transacción** | **object**   |        |
| transaction.gateway_order                | Número de la orden de compra. Id de transacción que es enviada al  gateway de pago. **Este valor debe ser unico y maximo de 12 caracteres** | string       | Si       |
| transaction.reference_id                 | El código de referencia de la transacción. Representa el identificador de  la transacción en el sistema del comercio. | string       | No       |
| transaction.purchase_order                | El código de referencia de la transacción. Representa el identificador de  la transacción en el sistema del comercio. (para propositos de conciliación) | string       | Si       |
| transaction.description                  | Descripción de la compra                 | string       | Si       |
| transaction.soft_descriptor              | Descripción corta de la transacción      | string       | Si       |
| **transaction.amount**                   | **Grupo de campos que detalla los montos de la compra** | **object**   |
| transaction.amount.currency              | Código ISO de la moneda asociada al monto de la compra. | string       | Si       |
| transaction.amount.total                 | Monto total de la compra que será descontado de la tarjeta o cuenta del  cliente | number          | Si       |
| transaction.amount.details               | Detalles del monto de la compra          |              |
| transaction.amount.details.subtotal      | Monto de la compra sin incluir impuesto  | number          | Si       |
| transaction.amount.details.tax           | Monto total de los impuestos             | number          | Si       |
| transaction.amount.details.shipping      | Costo del despacho                       | number          | Si       |
| transaction.amount.details.shipping_discount | Monto de descuento en costo de despacho  | number          | Si       |
| **transaction.item_list**                | **Información del producto(s)**         | **object**   |
| **transaction.item_list.shipping_address** | **Dirección de despacho (compras con despacho a domicilio)** | **object**   |
| transaction.item_list.shipping_address.line1 | Direccion de despaho                     | string       | Si       |
| transaction.item_list.shipping_address.city | Ciudad donde se realizará el despacho    | string       | Si       |
| transaction.item_list.shipping_address.country_code | Código de país donde se efectúa el despacho | string       | Si       |
| transaction.item_list.shipping_address.phone | Número de teléfono para la recepción de los productos despachados | string       | Si       |
| transaction.item_list.shipping_address.type | Tipo de despacho                         | string       | Si       |
| transaction.item_list.shipping_address.recipient_name | Nombre de la persona que recibirá el producto | string       | Si       |
| transaction.item_list.shipping_method    | Método de despacho de la compra: Digital, | string       | Si       |
| **transaction.item_list.items**          | **Grupo de campos que detalla los productos o servicios de la compra** | **objeto**   |
| transaction.item_list.items.sku          | Código SKU                               | string       | Si       |
| transaction.item_list.items.name         | Nombre del producto                      | string       | Si       |
| transaction.item_list.items.description  | Descripción del producto                 | string       | Si       |
| transaction.item_list.items.quantity     | Cantidad                                 | string       | Si       |
| transaction.item_list.items.price        | Precio unitario                          | number          | Si       |
| transaction.item_list.items.tax          | Monto del impuesto del producto          | number          | Si       |
| **redirect_urls**                        | **Url de redirección dependiendo del estado de la captura una vez  finalizado el proceso de captura** | **objeto**   |
| redirect_urls.return_url                 | URL de notificación de pago exitoso      | string (url) | Si       |
| redirect_urls.cancel_url                 | URL de notificación de pago fallido      | string (url) | Si       |
| **additional_attributes**                | **Grupo de campos de uso exclusivo**     | **objeto**   |
| additional_attributes.insuranceCode      | Código de la Aseguradora                 | string       | No       |
| additional_attributes.insuranceName      | Nemotécnico de la Asegurado              | string       | No       |

El resultado de la llamada a la API de checkout, será una intención de pago en su estado inicial (created), que contendrá el, o los links HATEOAS relacionados con la llamada.

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
| payer.payer_info.is_guest                | Indica si es un cliente invitado o un cliente que hizo login en el comercio | string  |
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
| **redirect_urls**                        | **Url de redirección dependiendo del estado de la transacción una vez  finalizado el proceso de pago** | **objeto**   |
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
