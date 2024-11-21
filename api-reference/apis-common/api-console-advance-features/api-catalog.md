---
description: Access API catalogs
---

# API catalog (advanced feature)

### What are API catalogs?

API catalogs are like menus in restaurant. You will need to choose one accordingly to your demand and context. For customer testing/integration purpose before go-live, choose "UATC[^1]". UATC catalog is identical to PRODUCTION (same APIs) but a different key would be subscribed for testing. For partners you would need to access internal test API catalog (UAT).

<figure><img src="../../../.gitbook/assets/Capture d’écran du 2023-10-29 18-14-09.png" alt=""><figcaption></figcaption></figure>

### Catalogs kinds

<table data-full-width="false"><thead><tr><th>Production (PROD)</th><th width="289.3333333333333">Test/sandbox for customer (UATC)</th><th>Test for partners (UAT)</th></tr></thead><tbody><tr><td>Visible in public. </td><td>.Only visible once connected and by customers accounts</td><td>Visible by anyone connected</td></tr><tr><td>Need an API key and only for customers</td><td>Need an API key and only for customers</td><td>Need an API key and anyone can subscribe</td></tr><tr><td>For production purpose</td><td>For testing purpose before go-live. </td><td>For partners only!</td></tr></tbody></table>

[^1]: User Acceptance Test for Customers
