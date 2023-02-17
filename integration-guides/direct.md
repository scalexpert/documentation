---
description: How to integrate ScaleXpert products with APIs
---

# APIs

Donner ici des exemples d'intégration d'APis avec des snippets de codes (postman permet par examples de récupérer les snippets). expliquer que les APis sont à intégrer de préférence côté serveur. faire réfrence au site github et à postman pour y chercher les collections

````java
```javascript
var settings = {
  "url": "https://sso.sgmarkets.com/sgconnect/oauth2/access_token?grant_type=client_credentials&scope=openid api.epos-emerchant-initiate-customer-application.qa-testing  api.epos-emerchant-initiate-customer-application.v1",
  "method": "POST",
  "timeout": 0,
  "headers": {
    "Content-Type": "application/x-www-form-urlencoded",
    "Authorization": "Basic Nzk3ZDI0ZjQtNmZmMi00MmMwLTg5ZjMtMDFhMjk4OWEwYWU5OjNsMDRoYWNjNDRnOGtiZDNlaDY0ZmxkbWcxOWU="
  },
};

$.ajax(settings).done(function (response) {
  console.log(response);
});
```
````

{% embed url="https://github.com/baas-ecommerce" %}
ScaleXpert Github
{% endembed %}

{% embed url="https://baas-ecommerce.postman.co/workspace/BaaS-S01---Public~d9e06529-1b19-48e5-95e4-1c2dcf7f5d9d/overview" %}
ScaleXpert Postman
{% endembed %}
