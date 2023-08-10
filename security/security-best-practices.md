# Security best practices

(to be completed)

### Use client-credential flow at server side only

[Client-credential oAuth2](../api-reference/apis-common/authentication.md) flow  is designed for server side only. There is no user authentication involved in the process (server to server). Thus, make attention to the security of your application back-end because authorization and credentials will rely on it.&#x20;

{% hint style="danger" %}
Don't call APIs with client credential flow at client-side but at server side only. The authorization must be obtain by a server or BFF (back-for-front) and so only that server should call the API (avoiding exposing your credentials and access tokens at client side).
{% endhint %}
