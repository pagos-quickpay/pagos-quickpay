# ¿Cómo obtener el codigo QR para autorizar una transacción?

Una vez ejecutada la intención de pago se desplegará el listado de URLs, debes utilizar la URL con el nombre **qr_code**

```
curl -X GET \
  https://api.qa.peinau.fif.tech/checkout/payments/gateways/pagoinapp/credit/{id}/qr \
```

Obtendrás una respuesta similar a:

![Ejemplo de QR Code](pagos/images/qr_code.png)
