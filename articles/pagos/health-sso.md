# Health Check Obtener Token de Acceso

Puedes consultar el estado del servicio de la siguiente forma:

```
curl -X GET \
  https://api.sandbox.connect.fif.tech/sso/health
  
```

Cuando el status del servicio es **UP** recibirás una respuesta similar a:

```
{
  "status": "UP",
  "up_time": "08:00:49",
  "info": {
    "profile": "TEST",
    "name": "api-qpay-single-sign-on",
    "version": "1.0.31",
    "routePrefix": "/sso",
    "logging": {
      "level": "info"
    }
  }
}
```
Http status code: **200**
