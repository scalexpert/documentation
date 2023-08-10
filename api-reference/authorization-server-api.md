---
description: Version 1.0.0
---

# oAuth2 API

API name: `auth-server`

Scope "openid`"`

{% hint style="info" %}
You don't need to subscribe to this API. This is implicit by using a scope that use client-credential flow as it the case for all our scopes.&#x20;
{% endhint %}

`Path:` [`https://api.e-commerce.societegenerale.com/baas/prod/auth-server/api/v1`](https://api.e-commerce.societegenerale.com/baas/prod/auth-server/api/v1)

{% swagger src="../.gitbook/assets/swagger_baas-as_1.0.0 (1).yaml" path="/oauth2/token" method="post" %}
[swagger_baas-as_1.0.0 (1).yaml](<../.gitbook/assets/swagger_baas-as_1.0.0 (1).yaml>)
{% endswagger %}

Download swagger file:

{% file src="../.gitbook/assets/swagger_baas-as_1.0.0 (1).yaml" %}
swagger auth-server API
{% endfile %}

See samples [here](../integration-guides/integrations-modes/direct.md#authentication-and-authorization)
