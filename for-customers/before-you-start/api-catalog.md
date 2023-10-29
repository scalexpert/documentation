---
description: Select your API catalog
---

# API catalog

{% hint style="info" %}
API reference documentation is available in this guide [here](broken-reference).
{% endhint %}

### Why choosing a catalog

API catalogs are like menus in restaurant. You will need to choose one accordingly to your demand and context. For testing purpose before go-live, choose "UATC[^1]". UATC catalog is identical to PRODUCTION (same APIs) but a different keys would need to be subscribed for testing.

Thus, as a customer you would have two keys :key: one for tests (UATC) and another for production (PROD).&#x20;

<figure><img src="../../.gitbook/assets/Capture d’écran du 2023-10-29 18-14-09.png" alt=""><figcaption></figcaption></figure>

{% embed url="https://dev.scalexpert.societegenerale.com/en/prod" %}
Access API catalogs
{% endembed %}

### Catalogs kinds

<table data-full-width="false"><thead><tr><th>Production</th><th>Test for customer (UATC)</th><th>Sandbox (Not available)</th></tr></thead><tbody><tr><td>Visible in public. </td><td>Only visible once connected and by customers accounts (See <a href="on-boarding-api.md">On boarding guide</a>). </td><td>Visible by anyone connected</td></tr><tr><td>Need an API key and only for customers</td><td>Need an API key and only for customers</td><td>Need an API key and anyone can subscribe</td></tr><tr><td>For production purpose</td><td>For testing purpose before go-live. </td><td>For exploration (Have fun ! <span data-gb-custom-inline data-tag="emoji" data-code="1f602">😂</span>)</td></tr></tbody></table>

{% hint style="warning" %}
Sandbox catalog is not yet available.
{% endhint %}

[^1]: User Acceptance Test for Customers
