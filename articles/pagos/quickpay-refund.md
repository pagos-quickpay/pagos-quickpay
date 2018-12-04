## Ejemplo petición de devolución:

Para saber si la tarjeta tiene saldo suficiente se debe invocar el endpoint rel: “refund_method”
 
A continuación se presenta ejemplo de un JSON de respuesta obtenido al devolver una intención de pago a través de la API RESTful de checkout:

```
{
    "refundTxnId": "2341612",
    "refundCancelationCode": "168817602013",
    "refundResponseDescription": "Success",
    "refundResponseCode": 0,
    "message": "successful refund",
    "refunded_amount": 1000
}
```


