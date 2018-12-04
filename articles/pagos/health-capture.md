# Health Check Api Capture

Puedes consultar el estado del servicio de la siguiente forma:

```
curl -X GET \
  https://api.sandbox.connect.fif.tech/tokenization/health
  
```

Cuando el status del servicio es **UP** recibirás una respuesta similar a:

```
{
  "status": "UP",
  "up_time": "22:48:16",
  "info": {
    "profile": "TEST",
    "name": "api-qpay-capture-card",
    "version": "1.0.31",
    "routePrefix": "/tokenization",
    "logging": {
      "level": "debug"
    }
  }
}
```
Http status code: **200**
