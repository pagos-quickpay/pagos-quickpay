## Ejemplo petición payment_method": "QUICKPAY_CREDIT_DOC_ID"

```
curl -X POST \
  https://api.sandbox.connect.fif.tech/checkout/payments \
  -H 'authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJwcmltYXJ5c2lkIjoiMjhhZGI5OTktN2EyZS03MGI4LWMwOTItZTRjMTZhOWU5ZTBhIiwidW5pcXVlX25hbWUiOiJUb2lwYXRvLmNvbSIsImdyb3Vwc2lkIjoiQVBQTCIsImlzcyI6IkZhbGFiZWxsYSIsImF1ZCI6IldlYiIsInR5cGUiOiJCZWFyZXIiLCJzY29wZSI6W10sImlhdCI6MTUxMzE3Nzk1OCwiZXhwIjoxNTEzMTc4ODU4fQ.OYBksNEvNBU012fJt4IhUnQ5g0szPXPmivD2GvprLczjbG6Pd7HeSyWddSCVOAwAXfycNMzwn0nb_6VdYMqbSzE3T9Bu0Oqzih4b_BfLLb4EwpRQ3L0ObFNkJTI2hfIMUNJQ5ohT8b2yR-1SiehAUd0Tlkb3zrh2aDP9AYVZGqkjLdnwQOpBtXVs6VmntXnb3_MklOU7U0BylB1kVG40t9qfSxf79DYTcr3JWs6LdCFDThkudMZtJfnjYsOoqt--Iv8BzhCU7Eft1Isf2Qfqn_1-p778E7r4yQY1GREuAsXPNfnnHxi7gOVVQ1owq1aekqt4m4ML-VLow8pUx5duYw' \
  -H 'content-type: application/json' \
  -d '{
  "payer": {
    "payer_info": {
      "email": "aroa@gmail.com",
      "full_name": "Andres Roa",
      "country": "CL",
      "document_number": "346055871",
      "document_type": "RUT",
      "is_guest": "true"
    },
    "payment_method": "QUICKPAY_CREDIT_DOC_ID"
  },
  "transaction": {
    "reference_id": null,
    "description": "Smartv",
    "soft_descriptor": "Sony Smartv",
    "amount": {
      "currency": "CLP",
      "total": 7200,
      "details": {
        "subtotal": 7200,
        "tax": 0,
        "shipping": 0,
        "shipping_discount": 0
      }
    },
    "item_list": {
      "shipping_address": {
        "line1": "Av. Las Condes 0225, Las Condes",
        "city": "Chile",
        "country_code": "CL",
        "phone": "+56955545899",
        "type": "HOME_OR_WORK",
        "recipient_name": "Andres Roa"
      },
      "shipping_method": "PICK_IN_PLACE",
      "items": [
        {
          "sku": "117110",
          "name": "TV Sony",
          "description": "TV Sony",
          "quantity": 1,
          "price": 7200,
          "tax": 0
        }
      ]
    },
    "gateway_order": "900000065434"
  },
  "redirect_urls": {
    "return_url": "https://web.segurosfalabella.com/co/",
    "cancel_url": "https://www.falabella.com.co/falabella-co/"
  },
  "intent": "sale",
  "additional_attributes": {
    "installments_offer": [
      "1",
      "3"
    ],
    "installments_without_interest": [
    ],
    "default_installment_number": "1",
    "default_deferred_month": "3",
    "is_deferred_capture": "false"
  }
}'
 
```

**Detalle de los Campos de la Petición**

| Nombre                                   | Descripción                              | Tipo                          |    Requerido | Cybersource |
| ---------------------------------------- | ---------------------------------------- | ----------------------------- | ------------ | ------------ |
| intent                                   | Identifica en tipo de transacción: Venta | string                        | Si           |               |
| **payer**                                | **Pagador**                              | **object**                    |              |               |
| **payer.payer_info**                     | **Información del cliente que está comprando en el sitio del  comercio** | **object**   |  | |         |
| payer.payer_info.email                   | correo electrónico                       | string                        | Si       |                   |
| payer.payer_info.first_name              | nombre del cliente                       | string                        | Si       |                   |
| payer.payer_info.last_name               | apellido del cliente                     | string                        | Si       |                   |
| payer.payer_info.country                 | Nacionalidad                             | string                        | Si       |                   |
| payer.payer_info.document_number         | Número de identificación                 | string                        | Si       |                   |
| payer.payer_info.document_type           | Tipo de documento de identificación      | string                        | Si       |                   |
| payer.payer_info.qp_user_id              | Token del cliente registrado en sistema Quickpay | string                | No       |                No |
| payer.payer_info.phone                   | Número telefonico del cliente            | string                        | No       |                   |
| payer.payer_info.is_guest                | Indica si es un cliente invitado o un cliente que hizo login en el comercio | string  | No       |     |
| payer.payer_info.gender                  | Nacionalidad                             | string                        | No       |                Si |
| payer.payer_info.age                     | Nacionalidad                             | string                        | No       |                Si |
| payer.payer_info.session_id              | Nacionalidad                             | string                        | No       |                Si |
| payer.payer_info.session_attempt_count   | Nacionalidad                             | string                        | No       |                Si |
| payer.payer_info.taxpayer_identity       | Nacionalidad                             | string                        | No       |                Si |
| payer.payment_method                     | Identifica el método de captura a utilizar (PEINAU_CAPTURE)  | string      | Si       | |
| **transaction**                          | **Grupo de campos con la información de la transacción** | **object**   |        | |
| transaction.gateway_order                | Número de la orden de compra. Id de transacción que es enviada al  gateway de pago. **Este valor debe ser unico y maximo de 12 caracteres** | string       | Si       | |
| transaction.reference_id                 | El código de referencia de la transacción. Representa el identificador de  la transacción en el sistema del comercio. | string       | No       | |
| transaction.description                  | Descripción de la compra                 | string       | Si       | |
| transaction.soft_descriptor              | Descripción corta de la transacción      | string       | Si       | |
| transaction.purchase_order                | El código de referencia de la transacción. Representa el identificador de  la transacción en el sistema del comercio. (para propositos de conciliación) | string       | Si       | |
| **transaction.amount**                   | **Grupo de campos que detalla los montos de la compra** | **object**   | |
| transaction.amount.currency              | Código ISO de la moneda asociada al monto de la compra. | string       | Si       | |
| transaction.amount.total                 | Monto total de la compra que será descontado de la tarjeta o cuenta del  cliente | number          | Si       | |
| transaction.amount.details               | Detalles del monto de la compra          |              | | |
| transaction.amount.details.subtotal      | Monto de la compra sin incluir impuesto  | number          | Si       | |
| transaction.amount.details.tax           | Monto total de los impuestos             | number          | Si       | |
| transaction.amount.details.shipping      | Costo del despacho                       | number          | Si       | |
| transaction.amount.details.shipping_discount | Monto de descuento en costo de despacho  | number          | Si       | |
| **transaction.item_list**                | **Información del producto(s)**         | **object**   | | |
| **transaction.item_list.shipping_address** | **Dirección de despacho (compras con despacho a domicilio)** | **object**   | | |
| transaction.item_list.shipping_address.line1 | Direccion de despaho                     | string       | Si       | |
| transaction.item_list.shipping_address.city | Ciudad donde se realizará el despacho    | string       | Si       | |
| transaction.item_list.shipping_address.country_code | Código de país donde se efectúa el despacho | string       | Si       | |
| transaction.item_list.shipping_address.phone | Número de teléfono para la recepción de los productos despachados | string       | Si       | |
| transaction.item_list.shipping_address.type | Tipo de despacho                         | string       | Si       | |
| transaction.item_list.shipping_address.recipient_name | Nombre de la persona que recibirá el producto | string       | Si       | |
| transaction.item_list.shipping_method    | Método de despacho de la compra: Digital, | string       | Si       | |
| **transaction.item_list.items**          | **Grupo de campos que detalla los productos o servicios de la compra** | **objeto**   | | |
| transaction.item_list.items.sku          | Código SKU                               | string       | Si       | |
| transaction.item_list.items.name         | Nombre del producto                      | string       | Si       | |
| transaction.item_list.items.description  | Descripción del producto                 | string       | Si       | |
| transaction.item_list.items.quantity     | Cantidad                                 | string       | Si       | |
| transaction.item_list.items.price        | Precio unitario                          | number          | Si       | |
| transaction.item_list.items.tax          | Monto del impuesto del producto          | number          | Si       | |
| **redirect_urls**                        | **Url de redirección dependiendo del estado de la captura una vez  finalizado el proceso de captura** | **objeto**   | | |
| redirect_urls.return_url                 | URL de notificación de pago exitoso      | string (url) | Si       | |
| redirect_urls.cancel_url                 | URL de notificación de pago fallido      | string (url) | Si       | |
| **additional_attributes**                | **Grupo de campos de uso exclusivo**     | **objeto**   | | |
| additional_attributes.return_url                 | URL de notificación de pago exitoso      | string (url) | Si       | |
| redirect_urls.cancel_url                 | URL de notificación de pago fallido      | string (url) | Si       | |
| **shipping_list**                        | **Grupo de campos que detalla  uso exclusivo**     | **objeto**   | | |

A continuación se presenta ejemplo de un JSON de respuesta obtenido al crear una intención de pago a través de la API RESTful de checkout:

```
{
    "application": "5af0799cd1aa8e000f9de4ca",
    "_id": "5bd1ddeabae25c0015cb050c",
    "additional_attributes": {
        "is_deferred_capture": "false",
        "default_deferred_month": "3",
        "default_installment_number": "1",
        "installments_without_interest": [
            "3"
        ],
        "installments_offer": [
            "1",
            "3"
        ]
    },
    "redirect_urls": {
        "return_url": "https://web.segurosfalabella.com/co/",
        "cancel_url": "https://www.falabella.com.co/falabella-co/"
    },
    "transaction": {
        "reference_id": null,
        "description": "Smartv",
        "soft_descriptor": "Sony Smartv",
        "gateway_order": "900000065434",
        "item_list": {
            "shipping_method": "PICK_IN_PLACE",
            "items": [
                {
                    "sku": "117110",
                    "name": "TV Sony",
                    "description": "TV Sony",
                    "quantity": 1,
                    "price": 7200,
                    "tax": 0
                }
            ],
            "shipping_address": {
                "line1": "Av. Las Condes 0225, Las Condes",
                "city": "Chile",
                "country_code": "CL",
                "phone": "+56955545899",
                "type": "HOME_OR_WORK",
                "recipient_name": "Andres Roa"
            }
        },
        "amount": {
            "currency": "CLP",
            "total": 7200,
            "details": {
                "subtotal": 7200,
                "tax": 0,
                "shipping": 0,
                "shipping_discount": 0
            }
        }
    },
    "payer": {
        "payer_info": {
            "is_guest": "true",
            "document_type": "RUT",
            "document_number": "346055871",
            "country": "CL",
            "full_name": "Andres Roa",
            "email": "aroa@gmail.com"
        },
        "payment_method": "QUICKPAY_CREDIT_DOC_ID"
    },
    "links": [
        {
            "href": "https://api.sandbox.connect.fif.tech/checkout/payments/5bd1ddeabae25c0015cb050c",
            "rel": "self",
            "method": "GET"
        },
        {
            "href": "https://api.sandbox.connect.fif.tech/checkout/payments/gateways/quickpay/credit_doc_id/5bd1ddeabae25c0015cb050c/pay",
            "rel": "approval_url",
            "method": "REDIRECT"
        },
        {
            "href": "https://api.sandbox.connect.fif.tech/checkout/payments/5bd1ddeabae25c0015cb050c/edit",
            "rel": "update_url",
            "method": "PUT"
        },
        {
            "href": "https://api.sandbox.connect.fif.tech/checkout/payments/gateways/quickpay/credit_doc_id/5bd1ddeabae25c0015cb050c/void",
            "rel": "void_method",
            "method": "POST"
        },
        {
            "href": "https://api.sandbox.connect.fif.tech/checkout/payments/gateways/quickpay/credit_doc_id/5bd1ddeabae25c0015cb050c/refund",
            "rel": "refund_method",
            "method": "POST"
        },
        {
            "href": "https://api.sandbox.connect.fif.tech/checkout/payments/900000065434",
            "rel": "self_by_gateway_order",
            "method": "GET"
        }
    ],
    "update_time": "2018-10-25T15:14:50.933Z",
    "create_time": "2018-10-25T15:14:50.933Z",
    "invoice_number": "IP-15404804909334111",
    "state": "created",
    "intent": "sale",
    "id": "5bd1ddeabae25c0015cb050c"
}
```
 
 
