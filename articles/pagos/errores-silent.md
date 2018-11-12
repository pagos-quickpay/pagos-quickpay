# Posibles Errores http code > 400 en la respuesta del Silent Charge

| HTTP code| Respuesta del servicio                   |
| -------- | ---------------------------------------- |
|400 | **error_code**: INVALID_MODEL, **error_description**: the requested model has invalid properties|
|401 | **error_code**: InvalidCredentials, **error_description**: No authorization token was found|
|401 | **error_code**: InvalidCredentials, **error_description**: caused by TokenExpiredError: jwt expired|
|401 | **error_code**: InvalidCredentials, **error_description**: caused by JsonWebTokenError: jwt malformed|
|404 | **error_code**: DOCUMENT_NOT_FOUND, **error_description**: The document you requested is not found|
| 500  |**error_code**: ERROR_WAITING_FOR_PROMISES_TO_RESOLVE, **error_description**: Exception has ocurred waiting for all promises to resolve when trying to approve payments|
| 500 | **error_code**: REQUEST_ERROR, **error_description**: Exception has ocurred when trying tokenize the credit card in cybersource|
| 500 | **error_code**: GATEWAY_DATA_DONT_EXISTS, **error_description**: Exception ocurred when trying to read the cybersource response: reply message from cybersource is empty|
| 500 | **error_code**: CYBERSOURCE_MISSING_REPLY, **error_description**: The response in cybersource has some invalid values|
| 500 | **error_code**: PEINAU_PAYMENT_UPDATE_ERROR, **error_description**: Exception ocurred when trying to update the payment after cybersource update|
| 500 | **error_code**: GATEWAY_DATA_DONT_EXISTS, **error_description**: Cybersource SOAP Message from cybersource or has some missing information|
|500 | **error_code**: DATABASE_ERROR, **error_description**: unknown error has ocurred when trying to get a payment by his id |
|500 | **error_code**: GENERAL_SYSTEM_ERROR |
|500 | **error_code**: PEINAU_ERROR |
|502 | **error_code**: Bad Gateway|
|503 | **error_code**: Service Temporarily unavailable, **error_description**: Service unavailable |
|503 | **error_code**: Service Temporarily unavailable, **error_description**: name resolution failed |
