# Security best practices

(to be completed)

### Use client-credential flow at server side only

[Client-credential oAuth2](../api-reference/apis-common/authentication.md) flow  is designed for server side only. There is no user authentication involved in the process (server to server). Thus, make attention to the security of your application back-end because authorization and credentials will rely on it.&#x20;

{% hint style="danger" %}
Don't call APIs with client credential flow at client-side but at server side only. The authorization must be obtain by a server or BFF (back-for-front) and so only that server should call the API (avoiding exposing your credentials and access tokens at client side).
{% endhint %}

### Store your secret in a designed secret management solution

Store secrets in a designated secrets management solution. For example, you can use a solution offered by your (cloud) infrastructure provider, such as [AWS Secrets Manager](https://aws.amazon.com/secrets-manager/), [Google Secrets Manager](https://cloud.google.com/secret-manager), or [Azure KeyVault](https://azure.microsoft.com/nl-nl/services/key-vault/). Another option is a dedicated secrets management system, such as [Hashicorp Vault](https://www.vaultproject.io/), [Keeper](https://www.keepersecurity.com/), [Confidant](https://lyft.github.io/confidant/), [Conjur](https://www.conjur.org/).&#x20;



{% hint style="danger" %}
Don't store secrets (and client id) in clear in the code. Best solution is to use a designed secret management solution. Alternatively, you can store it as encrypted field in your database.
{% endhint %}
