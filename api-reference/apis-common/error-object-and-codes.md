---
description: Error code structure & errors codes
---

# Error object & codes

### Generic structure of messages

All messages returned will be structured as below:

{% code title="Get internal server error" %}
```json
{
  "timestamp": "2022-07-28T22:25:51.000Z",
  "httpStatusCode": "500",
  "httpStatusMessage": "Internal Server Error",
  "errorMessage": "Une erreur est survenue",
  "requestMethod": "POST",
  "requestURI": "/v1/subscriptions"
}
```
{% endcode %}

{% code title="Error object structure" %}
```yaml
 GenericErrorResponse:
      title: GenericErrorResponse
      type: object
      properties:
        timestamp:
          type: string
          description: Timestamp of the error (ISO 8601 format)
          format: date-time
          example: '2022-07-28T22:25:51Z'
        httpStatusCode:
          type: integer
          description: HTTP Status code (404, 400, 500...)
          example: 400
        httpStatusMessage:
          type: string
          description: HTTP status message
          example: Bad Request
        errorCode:
          type: string
          description: >-
            The applicative error code. It is a machine readable code. Used when
            BAD_REQUEST error to provide details about the error
          example: INVALID_EMAIL
        errorMessage:
          type: string
          description: >-
            The applicative error message. It is a human readable English
            message
          example: The email address is not valid !
        requestMethod:
          type: string
          description: HTTP verb used to make the request. GET, POST, PUT, DELETE...
          example: GET
        requestURI:
          type: string
          description: URI of the request
          example: /v1/crédit
```
{% endcode %}
