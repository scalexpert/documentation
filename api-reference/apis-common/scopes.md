---
description: Authorization scopes overview
---

# Scopes

APIs are referring authorization scopes. For instance, [e-Financing API ](../e-financing-api/)refers to scope `"e-financing:rw"` allowing all operations endpoints. Scopes are required for subscription and to get access token.&#x20;

The list of scopes available are listed in the developer portal.

<figure><img src="../../.gitbook/assets/image (16).png" alt=""><figcaption><p>Search scopes  in the developer portal</p></figcaption></figure>

Scope define consumption levels (rate limit) and the authorizations flows for all related APIs. As of today, it exists one custom level 600 hits per minutes defined as standard consumption for all APIs. Authorization flow is always "client credentials".&#x20;

<figure><img src="../../.gitbook/assets/image (15).png" alt=""><figcaption><p>Scope "e-financing:rw"</p></figcaption></figure>

Link to access scope "e-financing:rw" in the developer portal:

{% embed url="https://dev.e-commerce.societegenerale.com/en/prod/scope/e-financing:rw" %}
Access scope "e-financing:rw" in the portal
{% endembed %}
