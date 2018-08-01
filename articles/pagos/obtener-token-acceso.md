## 1. Obtener un Token de Acceso

Te entregaremos dos llaves con las cuales te podrás autenticar en el sistema, a estas les llamamos **client_id** (identificador) y **client_secret** (Clave Secreta).

Con estas credenciales, deberás obtener un **token de acceso** enviando por medio del encabezado **Authorization** las credenciales bajo el formato client_id:client_secret al servidor de autorización. 

El servidor de autorización intercambiara las llaves del aplicativo por un token de acceso (**access_token**) válido para ejecutar requerimientos a nuestras a APIs RESTful. 

**Ejemplo:**
```
export CLIENT_ID=641281901508761220281
export CLIENT_SECRET=B8WKRXMiWHHrMCectt9Rg3ju4Y8GNheEa50gx6365sBV
curl -v -X POST https://api.sandbox.connect.fif.tech/sso/oauth2/v2/token \
 -H "Content-Type:application/x-www-form-urlencoded" \
 -H "Authorization: Basic $CLIENT_ID:$CLIENT_SECRET" \
 -d "grant_type=client_credentials" | json_pp
```

> El **CLIENT_ID** y **CLIENT_SECRET** utilizados en esta petición son datos de prueba.

Como respuesta obtendrás el **access_token**:

```
{  
   "scope":"",
   "token_type":"Bearer",
   "access_token":"eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJwcmltYXJ5c2lkIjoiMjhhZGI5OTktN2EyZS03MGI4LWMwOTItZTRjMTZhOWU5ZTBhIiwidW5pcXVlX25hbWUiOiJHbWFpbCIsImdyb3Vwc2lkIjoiQVBQTCIsImlzcyI6IkZhbGFiZWxsYSIsImF1ZCI6IldlYiIsInNjb3BlIjpbXSwiaWF0IjoxNTA4ODExNzA2LCJleHAiOjMwMTc3MDk4MTJ9.MQJFaXB-TWYbPGeJYU5CYcYJmc8mtERokeEgNSq31IjnIWvPugpD1lA0vU1zTsCTJJxb-jMfQGLqYb68HjMrZPiaFk09HZTWjdKEdWyV07Ospv4BwtVEfSlFBw-hVoazIYXng4UNXGQwxhMEduHyRY4yB6Anc2vk6J_EBPTkGv75ogsYl6bt1NTSZ9oHkjhz8Mp05Re7lt59XRajSFYp9OJExHjMJOS3mQw-zwwJedKua9XcdNu65Zx-8Zur7pcU_qk9Bjbd5o5D6Y5R6ueYUQx7kWnabWgt8ubDsEqRTnqUDvcY-5KYmMKXjtFD6riMWGXyX3EaOPNvYwrFNoXH9A",
   "expires_in":1508898106
}
```

[Consultar estado del servicio (Health Check)](health-sso.md)

Ir al paso [2. Crear una Intención de pago](crear-intencion-pago.md)
