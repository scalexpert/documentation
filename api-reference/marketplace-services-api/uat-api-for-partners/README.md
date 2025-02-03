---
description: Version 1.4.0 Latest
---

# 🆕 Marketplace Services API

[Download OpenAPI specs (YAML)](./#download-openapi-specs)

## 1 - Sellers on boarding

### Description

* Merchant registers sellers
* Merchant registers all sellers contacts
* Merchant registers all merchant documents
* Merchant registers all contacts documents
* Merchant submit a seller for KYC validation when all information required is complete.
* Merchant ask seller for IBAN verification
* Bank will provide KYC result (OK, KO, INCOMPLETE)

### Endpoints

{% content-ref url="endpoints-sellers-on-boarding.md" %}
[endpoints-sellers-on-boarding.md](endpoints-sellers-on-boarding.md)
{% endcontent-ref %}

## 2- Cash management

### **Description**

* The Marketplace Services API is used to execute the payment process from order until the payout.
* It offers the ability to register orders, transactions and then apply order-splits, transfers and payouts.
* Once the order is registered, the marketplace associates the transactions with the order. Then, the marketplace allocates funds to each seller and charges fees through the order-splits endpoint.
* Finally, the marketplace can make payments to the seller's external account or to its own external account.
* The endpoint /transfers provides the ability for the Marketplace to move funds between the seller account and the Marketplace account or vice versa.

### Endpoints

{% content-ref url="endpoints-cash-management.md" %}
[endpoints-cash-management.md](endpoints-cash-management.md)
{% endcontent-ref %}

### Download OpenAPI specs:

{% file src="../../../.gitbook/assets/swagger_marketplace_1.4.0-UATC.yaml" %}
YAML Marketplace Services for UATC
{% endfile %}

{% file src="../../../.gitbook/assets/swagger_marketplace_1.4.0-PROD.yaml" %}
YAML Marketplace Services for PROD
{% endfile %}
