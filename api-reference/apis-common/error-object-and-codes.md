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

### Standard codes and errors codes

<details>

<summary>Standard success codes</summary>

Reply 2xx when request behaves correctly as expected and documented:&#x20;

Code

Message

Semantic

200

OK

Usual OK, also to use for empty list and pagination. Must contain a body.

201

Created

Resource created from a POST, or also a PUT when the identifier can be pre-defined

202

Accepted

Asynch request with further treatment, polling or webhook may be used to get result

204

No content

There is no data to reply so response body is empty (not to use for empty list)

206

Partial Content

Unable to return all expected data for known reasons described in documentation

Do not use 206 for paging : when client request a page and you return it, you fully replied to its request.

</details>

<details>

<summary>Standard error codes</summary>

400

Bad request

Url does not match an endpoint, invalid parameter name or value, missing parameter, anything within body input fields/values that does not comply with documentation. => Client app developer MUST correct its code to avoid this errors.&#x20;

401

Unauthorized

Client app or end-user authentication is missing, invalid, expired, incomplete or at insufficient level, and must be re-done properly. More generally the system was not able to validate the requester. => Client app developer MUST correct its code to avoid this errors.&#x20;

403

Forbidden

The rights of the Client app or end-user are not sufficient as per the IAM system Warning: cases when end-user authentication is required but not possible because the received token is not containing end user information will result in 403 error. => Client app developer MUST correct its code to avoid this error and ensure it has rights to do the operation before triggering it. 404

Not found

Requested resource does not exists (only for a request on a specific resource id) => Client app developer MUST correct its code or data to avoid this error and ensure the identifier it uses are valid&#x20;

405

Method Not Allowed

HTTP verb is not allowed on this resource endpoint => Client app developer MUST correct its code to avoid this errors.&#x20;

406

Not Acceptable

Client ask for an invalid response content-type => Client app developer MUST correct its code to avoid this errors.&#x20;

410

Gone

Client ask to remove a resource that was already removed and cannot be recreated => Client app developer MUST correct its code or data to avoid this error and ensure the identifier it uses are valid&#x20;

409

Conflict

There is data conflict on a modification request (eg: old data version, lock, already exists), that the client (user or program) can solve somehow, he then can retry same or similar modif => Client app developer MUST correct its code or data to avoid this error and ensure the identifier it uses are valid&#x20;

429

Too Many Requests

A quota/throttling logic detected too many requests from client in current period => Client app developer MUST prevent itself to call the API beyond its allowed quota Since the status code may match several use cases you should Use standardized error body to give sufficient information in the response body so the client app developer team can alone understand the issue and correct its code or data.

</details>





