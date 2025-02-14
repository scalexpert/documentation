---
description: e-financing error codes reference
---

# e-financing error codes

### Error codes

#### Error codes are application  codes that are returned in the response body when the HTTP status code is 4XX.  This code is machine readble and represents the cause of the error.

#### **The error codes when the Http status  is 400 Bad request**

1. **Error codes returned by all e-financing endpoints :**

| Error  code                | Error Description                                                                                                                                                                                                                                                                                                                                    | Recomended handling                                                                                                                                                |
| -------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| REQUEST\_VALIDATION\_ERROR | <p>A generic error for an invalid format in any field of the request body. This error occurs when the input value does not match the defined format of a field in the body of a POST, PATCH, or PUT request.    </p><p>Example of error message: buyers[0].contactAddress.phoneNumber is invalid. It must match the pattern ^\+[1-9]\d{1,14}$   </p> | <p>The consumer <strong>must</strong> follow the format specifications outlined in the <a href="./">Swagger documentation</a>.</p><p> </p>                         |
| INVALID\_COUNTRY\_CODE     | A specific error code is returned when an input field representing a country does not match the ISO 3166-1 alpha-2 format.                                                                                                                                                                                                                           | The consumer **must** provide the country code in the[ ISO 3166-1 alpha-2 format](https://www.iso.org/iso-3166-country-codes.html) (Two-letters currency codes )   |
| INVALID\_CURRENCY\_CODE    | A specific error code is returned when an input field representing a currency does not match  the three-letter currency codes defined by ISO 4217 alpha-3.                                                                                                                                                                                           | The consumer **must** provide the currency code in the  [ISO 4217 alpha-3 format ](https://www.iso.org/iso-4217-currency-codes.html)(Three-letter currency codes ) |
| INVALID\_PAGE\_INDEX       | This error code typically occurs when the request parameter 'page' is less than 1.                                                                                                                                                                                                                                                                   | The consumer **must** provide a page value greater than or equal to 1.                                                                                             |
| INVALID\_UUID              | This error code typically occurs when the request path parameter 'subscriptionId' is not an uuid.                                                                                                                                                                                                                                                    | Consumer  **must** provide a subscriptionId in  a format of uuid.                                                                                                  |

2. **Specific error codes  related to  the  POST /subscriptions:**

| Error  code                                                                                 | Error Description                                                                                                                                                          | Recomended handling                                                                                                                                                                                                         |
| ------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| FORBIDDEN                                                                                   | This error occurs when the merchant tries to invoke _**POST / subscriptions**_ with a solutionCode that is not eligible.                                                   | If this error occurs, the consumer **must** use one of the solutionCodes returned in the response of the GET /eligible-solutions request. Only these solutionCodes are eligible for use in the POST /subscriptions request. |
| REQUEST\_VALIDATION\_ERROR                                                                  | <p> </p><p>The phoneNumber and mobilePhoneNumber must be consistent with the marketCode of the solutionCode (e.g., FR, DE, etc.).                                     </p> | For example, when the marketCode is FR, the mobilePhoneNumber **must** start with the international code +33.                                                                                                               |
| BAD\_REQUEST (this error code will be replaced with another error code in the next version) | This error occurs when a subscription with the same merchantGlobalOrderId already exists.                                                                                  | merchantGlobalOrderId must be unique for each subscripton.                                                                                                                                                                  |

**Specific error codes  related to  the  POST /subscriptions/\_confirmDelivery:**

to be completed

**Specific error codes  related to  the  POST /subscriptions/\_cancel:**

to be completed



### Generic errors codes

{% content-ref url="../apis-common/error-object-and-codes.md" %}
[error-object-and-codes.md](../apis-common/error-object-and-codes.md)
{% endcontent-ref %}

