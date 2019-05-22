```
{
    "_id": "5be43bf2ce01180015ca6321",
    "expiration_date": "2018-11-08T13:37:50.700Z",
    "application": "5af0799cd1aa8e000f9de4ca",
    "payment_method": "WALLET_QR",
    "gateway": {
        "error": {
            "meta_data": {
                "payerDocumentNumber": "371119582",
                "totalAmount": 300,
                "curency": "CLP",
                "documentState": "created",
                "paymentMethod": "WALLET_QR",
                "gatewayOrder": "IP-15416842106589081",
                "paymentId": "5be43bf2ce01180015ca6321"
            },
            "error_description": "Payment intention is expired",
            "error_code": "EXPIRED_PAYMENT_INTENTION"
        }
    },
    "transaction": {
        "purchase_order": "IP15416826212839081",
        "description": "Compra COPEC Chesterton",
        "soft_descriptor": "COPEC-PAGO-CLICK",
        "reconciliation_id": "9182736633",
        "description": "Compra en Comercio X",
        "soft_descriptor": "PRODUCTO X",
        "invoice_type": "boleta",
        "invoice_number": "AB123456",
        "terminal_id": "1234567",
        "store_id": "102",
        "channel:" "WEB",
        "item_list": {
            "shipping_method": "DIGITAL",
            "items": [
                {
                    "sku": "GASOLINA",
                    "name": "Gas. 93",
                    "description": "Gasolina 93, 45lts",
                    "quantity": 1,
                    "price": 400,
                    "tax": 0
                },
                {
                    "sku": "DESCLIP",
                    "name": "Desc Socio",
                    "description": "Descuento Socio",
                    "quantity": 1,
                    "price": -50,
                    "tax": 0
                },
                {
                    "sku": "DESGASO93",
                    "name": "Desc Falabella",
                    "description": "Destalle Descuento Falabella",
                    "quantity": 1,
                    "price": -50,
                    "tax": 0
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
            "total": 300,
            "details": {
                "subtotal": 400,
                "tax": 0,
                "shipping": 0,
                "shipping_discount": 0
            }
        },
        "promotions": [
            {
              "type": "CMR",
              "amount": 300,
              "currency": "CLP",
            }
        ],
        "installments": {
            "installments_offer": [
               "1",
               "3",
               "6"
            ],
            "installments_without_interest": [  
               "3"
            ],
            "default_installment_number": "1"
        },
        "deferred_info": {
          "deferred_months": [
            "1", "2", "3"
        ],
        "default_deferred_month":"3",
        "selected_promotion": {
            "type": "CMR",
            "amount": 20000,
            "currency": "CLP"
        },
        "selected_payment_method": "WALLET_CREDIT"
    },
    "payer": {
        "email": "pperez@gmail.com",
        "full_name": "Pedro Perez",
        "country": "CL",
        "document_number": "371119582",
        "document_type": "RUT"
    },
    "links": [
        {
            "href": "https://api.sandbox.connect.fif.tech/checkout/payments/5be43bf2ce01180015ca6321",
            "rel": "self",
            "method": "GET"
        },
        {
            "href": "https://api.sandbox.connect.fif.tech/checkout/payments/gateways/pagoinapp/credit/5be43bf2ce01180015ca6321/pay",
            "rel": "approval_url",
            "method": "REDIRECT"
        },
        {
            "href": "https://api.sandbox.connect.fif.tech/checkout/payments/5be43bf2ce01180015ca6321/edit",
            "rel": "update_url",
            "method": "PUT"
        }
    ],
    "update_time": "2018-11-08T14:07:48.618Z",
    "create_time": "2018-11-08T13:36:50.658Z",
    "state": "expired",
    "intent": "sale",
    "id": "5be43bf2ce01180015ca6321"
}
```
