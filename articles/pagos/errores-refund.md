# Posibles rechazos Anulaciones / refund

## Formato de error en la respuesta del Gateway
| HTTP code| Respuesta del servicio                               |
| -------- | ---------------------------------------- |
|500 | **error_code**: GW01_XX, **error_description**: DESCRIPCION RETORNADA POR EL GATEWAY|

> Para este caso se debe consultar la [Lista de códigos de respuesta CyberSource](../pasarela-de-pagos/api-tokenizacion-pago/cybersource_reason_code.md). Donde XX del **error_code** será el reason code respectivo y en el **error_description** estará expresada la descripción de dicho reason code de acuerdo al Gateway.

## Formato de error que NO proviene del Gateway
| HTTP code| Respuesta del servicio                               |
| -------- | ---------------------------------------- |
|400 | **error_code**: INVALID_MODEL, **error_description**: the requested model has invalid properties|
|401 | **error_code**: InvalidCredentials, **error_description**: caused by TokenExpiredError: jwt expired|
|401 | **error_code**: InvalidCredentials, **error_description**: caused by JsonWebTokenError: jwt malformed|
|404 | **error_code**: DOCUMENT_NOT_FOUND, **error_description**: The document you requested is not found|
| 500  |**error_code**: PAYMENT_IN_CREATED_STATE_CANT_BE_REFUNDED, **error_description**: A capture in created state cant be refunded|
| 500 | **error_code**: PAYMENT_IN_REJECTED_STATE_CANT_BE_REFUNDED, **error_description**: A capture in reject state cant be refunded |
| 500 | **error_code**: PAYMENT_ALREADY_REFUNDED, **error_description**: The capture or credit is not refund because the capture or credit information has already been submitted to your processor. Or, you requested a refund for a type of transaction that cannot be refunded. |
| 500 | **error_code**: CYBERSOURCE_MISSING_REPLY, **error_description**: The response in cybersource has some invalid values|
| 500 | **error_code**: REFUNDED_AMOUNT_HIGHER_PAYMENT_TOTAL, **error_description**: The refunded amount can not be higher than payment total. |
| 500 | **error_code**: GATEWAY_DATA_DONT_EXISTS, **error_description**: Cybersource SOAP Message from cybersource or has some missing information|
|500 | **error_code**: DATABASE_ERROR, **error_description**: unknown error has ocurred when trying to get a payment by his id |
|500 | **error_code**: GENERAL_SYSTEM_ERROR, **error_description**: Unknow error when trying to create a payment intention |
|500 | **error_code**: PEINAU_ERROR |
