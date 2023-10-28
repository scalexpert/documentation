---
description: Authentication overview
---

# Authentication

### Authentication oAuth2 client credentials flow

All our endpoints are authenticated with oAuth2 client credentials flow. It means APIs are application authenticated (server side). You would need to get a client id and secret to obtain a access token using our [API /oauth2/token ](../authorization-server-api.md).&#x20;

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption><p>Client credentials flow</p></figcaption></figure>

1. Application sends [application's credentials](../../developers-docs/before-you-start/api-key.md#3-api-key) to the oAuth2 Authorization Server with the [authorization scopes](scopes.md) you want to access.&#x20;
2. oAuth2 Authorization Server validates application's credentials.
3. oAuth2 Authorization Server responds with an access token.
4. Application can use the access token to call an API on behalf of itself.&#x20;
5. API responds with requested data.

{% hint style="warning" %}
Each token issued has a life time (see attribute expires\_in in the response) and you will have to issue a new token when the life time has expired.
{% endhint %}

For more details please refers to [RFC 6749](https://tools.ietf.org/html/rfc6749#section-3.2) .

See API reference there:

{% content-ref url="../authorization-server-api.md" %}
[authorization-server-api.md](../authorization-server-api.md)
{% endcontent-ref %}



&#x20;
