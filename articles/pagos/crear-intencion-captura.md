## 2. Intención de Captura

Para generar una intención de captura debes hacer una petición a la API de **Intención de Captura /captures** con el **access_token** generado en el [paso 1](obtener-token-acceso.md) y el JSON correspondiente al metodo de pago que quieras emplear.

- Captura CMR [Json ejemplo capture_method": "CMR_CAPTURE" ](json-capture-quickpay-credit.md)


**Detalle de las URLs generadas:**

- **self**: desde esta URL puedes consultar la información de la intención de pago. [Ejemplo de ejecución de Self](self.md).
- **capture**: desde esta se debe tokenizar/capturar tarjeta [Ejemplo de ejecución del capture](capture.md).

> Estas URLs son dinamicas, nunca debes guardarlas como variables de entorno. Siempre debes consultarlas desde aquí para continuar con los pasos siguientes.

[Consultar estado del servicio (Health Check)](health-capture.md)
