---
description: All frequent questions on integration
---

# FAQ

### Integration questions

#### 1-How to get "Id" of the command when e-buyer is redirected on the confirmation page? 

Several methods are possible: \
1-When subscribing, the merchant transmits the order reference in the request (`merchantGolbalOrderId`) and also a redirection URL for the confirmation page (`merchantUrls/confirmation`) see [API documentation](../../api-reference/e-financing-api/).\
2-in response, the merchant receives a subscription number (id) which he must keep. The customer is redirected and starts the credit or payment process. At the end of the process or abandonment or error, the client is redirected to the confirmation URL transmitted as a parameter during the initialization request. \
3-To retrieve the order at this time, several solutions are possible: \
a-If the merchant has transmitted a parameter in the confirmation URL (https://monsite.com?parameter=xxxxxx) he will retrieve it. \
b-If the merchant has a session cookie and the “same-site = Lax” strategy he will recover the session cookie (see [Understanding SameSite cookies page](https://andrewlock.net/understanding-samesite-cookies/) to understand) \
c-(recommanded solution) Using the subscription number obtained previously, the merchant can obtain the status of the subscription (consolidatedStatus). It is recommended to apply a timeout to manage the desynchronization between the redirection and the status update. \
d-Upon receipt of the [webhook](../../webhooks/how-to-subscribe-use-webhooks.md) (IPN), the merchant will receive directly in the body of the request the subscription id (id), the order number (`merchantGlobalId`), the status (`consolidatedStatus`)
