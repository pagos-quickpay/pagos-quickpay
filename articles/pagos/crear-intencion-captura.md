## Intención de Captura de Tarjeta (Tokenización)

Para generar una intención de captura debes hacer una petición a la API de **Intención de Captura /captures** con el **access_token** generado en el [paso 1](obtener-token-acceso.md) y el JSON correspondiente al metodo de pago que quieras emplear.

- Captura de Tarjeta CMR [Json ejemplo capture_method": "CMR_CAPTURE" ](json-cmr-capture-intention.md)
- Captura de Tarjeta de Terceros (No CMR) [Json ejemplo capture_method": "PEINAU_CAPTURE" ](json-peinau-capture-intention.md)

[Consultar estado del servicio (Health Check)](health-capture.md)
