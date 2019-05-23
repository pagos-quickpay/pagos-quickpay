## Intención de Pago (Wallet)

Para generar una intención de pago debes hacer una petición a la API de **Intención de Pago /payments** con el **access_token** generado en el [paso 1](obtener-token-acceso.md) y el JSON correspondiente al metodo de pago que quieras emplear.

- Wallet QR [Json ejemplo payment_method: "WALLET_QR" ](json-wallet-qr.md)
- Wallet CASH [Json ejemplo payment method: "WALLET_CASH"](json-wallet-cash.md)

**Detalle de los Campos de la Petición**

| Nombre                                   | Descripción                              | Tipo         |    Requerido |
| ---------------------------------------- | ---------------------------------------- | ------------ | ------------ |
| intent                                   | Identifica en tipo de transacción: Venta | string       | Si           |
| payment_method                     | Identifica el método de pago a utilizar (WALLET_QR)  | string       | Si       |
| **payer**                     | **Información del cliente que está comprando en el sitio del  comercio** | **object**   |
| payer.email                   | correo electrónico                       | string       | Si       |
| payer.full_name               | nombre completo                          | string       | Si       |
| payer.country                 | Nacionalidad                             | string       | Si       |
| payer.document_number         | Número de identificación                 | string       | Si       |
| payer.document_type           | Tipo de documento de identificación      | string       | Si       |
| **transaction**                          | **Grupo de campos con la información de la transacción** | **object**   |       
| transaction.purchase_order                | Id de transacción que es enviada al  gateway de pago. **Este valor debe ser unico** | string       | Si       |
| transaction.reconciliation_id                 | El código de referencia de la transacción. Representa el identificador de  la transacción en el sistema del comercio. | string       | No       |
| transaction.description                  | Descripción de la compra                 | string       | Si       |
| transaction.soft_descriptor              | Descripción corta de la transacción      | string       | Si       |
| transaction.invoice_type                  | Tipo de documento boleta/factura                 | string       | Si       |
| transaction.invoice_number                  | Número de boleta                 | string       | Si       |
| transaction.terminal_id                  | Identificador del terminal                 | string       | Si       |
| transaction.store_id                  | Identificacion de la tienda                | string       | Si       |
| transaction.channel                  | Canal de compra                 | string       | Si       |
| **transaction.amount**                   | **Grupo de campos que detalla los montos de la compra** | **object**   |
| transaction.amount.currency              | Código ISO de la moneda asociada al monto de la compra. | string       | Si       |
| transaction.amount.total                 | Monto total de la compra que será descontado de la tarjeta o cuenta del  cliente | number          | Si       |
| transaction.amount.details               | Detalles del monto de la compra          |              |
| transaction.amount.details.subtotal      | Monto de la compra sin incluir impuesto  | number          | Si       |
| transaction.amount.details.tax           | Monto total de los impuestos             | number          | Si       |
| transaction.amount.details.surcharge     | Recargo financiero                       | number          | Si       |
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
| **transaction.item_list.items**          | **Grupo de campos que detalla los productos o servicios de la compra. Solo se pemite un producto para compra con puntos.** | **objeto**   |
| transaction.item_list.items.sku          | Código SKU                               | string       | Si       |
| transaction.item_list.items.name         | Nombre del producto                      | string       | Si       |
| transaction.item_list.items.description  | Descripción del producto                 | string       | Si       |
| transaction.item_list.items.quantity     | Cantidad.  Solo se pemite un producto para compra con puntos.      | string       | Si       |
| transaction.item_list.items.price        | Precio unitario                          | number          | Si       |
| transaction.item_list.items.tax          | Monto del impuesto del producto          | number          | Si       |
| **promotions**      | Listado de Promociones                    | **array**   | No       |
| promotions.type     | Tipo de Promoción                        | string       | No       |
| promotions.amount   | Monto correspondiente a la promoción       | number       | No       |
| promotions.currency | Código ISO de la moneda asociada al descuento | string  | No       |
| **installments**                | **Grupo de campos para informacion de cuotas**     | **objeto**   |
| installments.installments_offer | Listado de cuotas habilitadas por el comercio | **array** | No    |
| installments.installments_without_interest | Listado de cuotas sin interes | **array** | No    |
| installments.default_installment_number | Cantidad de cuotas por default | string | No   |
| **deferred_info**                | **Grupo de campos para informacion de mes diferido**     | **objeto**   |
| deferred_info.deferred_months | Cantidad de  cuotas diferidas para el pago de la primera cuota | array | No   |
| deferred_info.default_deferred_month | Cantidad de  cuotas diferidas para el pago de la primera cuota | string | No   |
| **additional_attributes**                | **Grupo de campos de uso exclusivo**     | **objeto**   |

El resultado de la llamada a la API de checkout, será una intención de pago en su estado inicial (created), que contendrá el, o los links HATEOAS relacionados con la llamada.

**Detalle de los campos de la Respuesta**

| Nombre                                   | Descripción                              | Tipo         |
| ---------------------------------------- | ---------------------------------------- | ------------ |
| intent                                   | Identifica en tipo de transacción: Venta | string       |
| payment_method                     | Identifica el método de pago a utilizar  | string       |
| **payer**                                | **Información del cliente que está comprando en el sitio del  comercio**                              | **object**   |
| payer.email                   | correo electrónico                       | string       |
| payer.full_name               | nombre completo                          | string       |
| payer.country                 | Nacionalidad                             | string       |
| payer.document_number          | Número de identificación                 | string       |
| payer.document_type            | Tipo de documento de identificación      | string       |
| **transaction**                          | **Grupo de campos con la información de la transacción** | **object**   |
| transaction.purchase_order                | Id de transacción que es enviada al  gateway de pago. **Este valor debe ser unico** | string       |
| transaction.reconciliation_id                 | El código de referencia de la transacción. Representa el identificador de  la transacción en el sistema del comercio. | string       |
| transaction.description                  | Descripción de la compra                 | string       |
| transaction.soft_descriptor              | Descripción corta de la transacción      | string       |
| transaction.invoice_type                  | Tipo de documento boleta/factura                 | string       |
| transaction.invoice_number                  | Número de boleta                 | string       |
| transaction.transaction_code  | Código alternativo para identificar la intención de pago | string  |
| transaction.terminal_id                  | Identificador del terminal                 | string       |
| transaction.store_id                  | Identificacion de la tienda                | string       |
| transaction.channel                  | Canal de compra                 | string       |
| **transaction.amount**                   | **Grupo de campos que detalla los montos de la compra** | **object**   |
| transaction.amount.currency              | Código ISO de la moneda asociada al monto de la compra. | string       |
| transaction.amount.total                 | Monto total de la compra que será descontado de la tarjeta o cuenta del  cliente | number          |
| transaction.amount.details               | Detalles del monto de la compra          |              |
| transaction.amount.details.subtotal      | Monto de la compra sin incluir impuesto  | number          |
| transaction.amount.details.tax           | Monto total de los impuestos             | number          |
| transaction.amount.details.surcharge     | Recargo financiero                       | number          |
| transaction.amount.details.shipping      | Costo del despacho                       | number          |
| transaction.amount.details.shipping_discount | Monto de descuento en costo de despacho  | number|
| **transaction.item_list**                | **Información del producto(s)**         | **object**   |
| **transaction.item_list.shipping_address** | **Dirección de despacho (compras con despacho a domicilio)** | **object**   |
| transaction.item_list.shipping_address.line1 | Direccion de despaho                     | string       |
| transaction.item_list.shipping_address.city | Ciudad donde se realizará el despacho    | string       |
| transaction.item_list.shipping_address.country_code | Código de país donde se efectúa el despacho | string       |
| transaction.item_list.shipping_address.phone | Número de teléfono para la recepción de los productos despachados | string       |
| transaction.item_list.shipping_address.type | Tipo de despacho                         | string       |
| transaction.item_list.shipping_address.recipient_name | Nombre de la persona que recibirá el producto | string       |
| transaction.item_list.shipping_method    | Método de despacho de la compra: Digital, | string       |
| **transaction.item_list.items**          | **Grupo de campos que detalla los productos o servicios de la compra.  Solo se pemite un producto para compra con puntos.** | **objeto**   |
| transaction.item_list.items.sku          | Código SKU                               | string       |
| transaction.item_list.items.name         | Nombre del producto                      | string       |
| transaction.item_list.items.description  | Descripción del producto                 | string       |
| transaction.item_list.items.quantity     | Cantidad:  Solo se pemite un producto para compra con puntos | string       |
| transaction.item_list.items.price        | Precio unitario                          | number          |
| transaction.item_list.items.tax          | Monto del impuesto del producto          | number          |
| **promotions**      | Listado de Promociones                    | **array**   |
| promotions.type     | Tipo de Promoción                        | string       |
| promotions.amount   | Monto correspondiente a la promoción       | number       |
| promotions.currency | Código ISO de la moneda asociada al descuento | string  |
| **installments**                | **Grupo de campos para informacion de cuotas**     | **objeto**   |
| installments.installments_offer | Listado de cuotas habilitadas por el comercio | **array** |
| installments.installments_without_interest | Listado de cuotas sin interes | **array** |
| installments.default_installment_number | Cantidad de cuotas por default | string |
| **deferred_info**                | **Grupo de campos para informacion de mes diferido**     | **objeto**   |
| deferred_info.deferred_months | Cantidad de  cuotas diferidas para el pago de la primera cuota | array |
| deferred_info.default_deferred_month | Cantidad de  cuotas diferidas para el pago de la primera cuota | string |
| **additional_attributes**                | **Grupo de campos de uso exclusivo**     | **objeto**   |
| ...               | ...    | **objeto**   |
| id                                       | Identificador unico de la intención      | string (Guid)|
| create_time                              | Fecha de creación de la intención        | string (ISO 8601)|
| update_time                              | Fecha de actualización de la intención   | string (ISO 8601)|
| application                              | Identificador interno    | string|
| **links** | Arreglo de Link HATEOAS para la ejecución de operaciones disponibles sobre la intención | array |
| **links.link** | Enlace bajo formato HATEOAS, sobre la definición de una operación disponible en una intención  | **objeto**  |
| links.link.href | Dirección URL de la operación | string (URL) |
| links.link.rel |Relación de la operación sobre una intención | Enum |
| links.link.method |Verbo HTTP solicitado para la ejecución de la operación|Enum|

**Detalle de las URLs generadas:**

- **self**: desde esta URL puedes consultar la información de la intención de pago. [Ejemplo de ejecución de Self](self.md).
- **approval_url**: desde esta URL el cliente debe autorizar el pago.
- **confirm**: desde esta URL se autorizar el pago.
- **qr_code**: esta URL genera automaticamente un codigo QR para autorizar un pago (Solo disponible para PagoInApp y Wallet). [Ejemplo de ejecución de Qr Code](qr_code.md).
- **self_by_gateway_order**: desde esta URL puedes consultar la información de la intención de pago.
- **self_by_transaction_code**: desde esta URL puedes consultar la información de la intención de pago.

> Estas URLs son dinamicas, nunca debes guardarlas como variables de entorno. Siempre debes consultarlas desde aquí para continuar con los pasos siguientes.

[Consultar estado del servicio (Health Check)](health-checkout.md)
