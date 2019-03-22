```
{
    "_id": "5c94fa02aebebc00168c6faa",
    "query": "CMR_POINTS",
    "application": "5b45235b9c98fc0fbdffadbd",
    "gateway": {
        "msgType": "PointsResponse",
        "responseCode": 0,
        "responseDescription": "Success",
        "UUID": "320ef0f6-87a6-4308-ae52-f781cca515a9",
        "data": {
            "kindOfPoints": "CMR_PUNTOS",
            "amountOfPoints": 0,
            "pointsToExpire": 0,
            "dateToExpire": "1991-01-01",
            "country": "CL",
            "documentType": "RUT",
            "documentId": "123451238"
        },
        "transactionId": "320ef0f6-87a6-4308-ae52-f781cca515a9"
    },
    "links": [
        {
            "href": "https://api.qa.peinau.fif.tech/query/queries/5c94fa02aebebc00168c6faa",
            "rel": "self",
            "method": "GET",
            "security": []
        },
        {
            "href": "https://api.qa.peinau.fif.tech/query/queries/gateways/cmr/points/5c94fa02aebebc00168c6faa/query",
            "rel": "query_url",
            "method": "REDIRECT",
            "security": []
        }
    ],
    "redirect_urls": {
        "return_url": "https://google.com",
        "cancel_url": "https://outlook.live.com/owa/"
    },
    "customer": {
        "country": "CL",
        "name": "Jose Galvans",
        "document_type": "RUT",
        "document_number": "123451238",
        "is_guest": false
    },
    "expiration_time": "1970-01-01T00:00:00.010Z",
    "update_time": "2019-03-22T15:07:11.418Z",
    "create_time": "2019-03-22T15:06:42.830Z",
    "state": "executed",
    "invoice_number": "QRY-1553267202830",
    "id": "5c94fa02aebebc00168c6faa"
}
```
