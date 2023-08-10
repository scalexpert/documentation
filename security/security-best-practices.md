# Security best practices

(to be completed)

### Use client-credential at server side only

[Client-credential oAuth2](../api-reference/apis-common/authentication.md) flow  is designed for server side only. There is no user authentication involved in the process (server to server). Thus, make attention the security rely on your application back-end security.&#x20;

{% hint style="danger" %}
Don't call APIs at client-side but at server side only.&#x20;
{% endhint %}
