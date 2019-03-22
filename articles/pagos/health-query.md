# Health Check Api query

Puedes consultar el estado del servicio de la siguiente forma:

```
curl -X GET \
  https://api.qa.peinau.fif.tech/query/health
  
```

Cuando el status del servicio es **UP** recibirás una respuesta similar a:

```
{
  "status": "UP",
  "up_time": "239:45:00",
  "info": {
    "profile": "TEST",
    "name": "peinau-api-query",
    "version": "1.0.0",
    "routePrefix": "/query",
    "logging": {
      "level": "info"
    }
  }
}
```
Http status code: **200**
