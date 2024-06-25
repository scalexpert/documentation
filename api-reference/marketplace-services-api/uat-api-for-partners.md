---
description: Version 1.0.5 Latest (only for partners )
---

# UAT API for partners

### Description

**Marketplace Services**

* The Marketplace Services API is used to execute the payment process from order until the payout.
* It offers the ability to register orders, transactions and then apply order-splits, transfers and payouts.
* Once the order is registered, the marketplace associates the transactions with the order. Then, the marketplace allocates funds to each seller and charges fees through the order-splits endpoint.
* Finally, the marketplace can make payments to the seller's external account or to its own external account.
* The endpoint /transfers provides the ability for the Marketplace to move funds between the seller account and the Marketplace account or vice versa.

### Orders

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.5_UAT.yaml" path="/orders" method="post" %}
[swagger_marketplace_1.0.5_UAT.yaml](../../.gitbook/assets/swagger_marketplace_1.0.5_UAT.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.5_UAT.yaml" path="/orders" method="get" %}
[swagger_marketplace_1.0.5_UAT.yaml](../../.gitbook/assets/swagger_marketplace_1.0.5_UAT.yaml)
{% endswagger %}

### Transactions

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.5_UAT.yaml" path="/transactions" method="post" %}
[swagger_marketplace_1.0.5_UAT.yaml](../../.gitbook/assets/swagger_marketplace_1.0.5_UAT.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.5_UAT.yaml" path="/transactions" method="get" %}
[swagger_marketplace_1.0.5_UAT.yaml](../../.gitbook/assets/swagger_marketplace_1.0.5_UAT.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.5_UAT.yaml" path="/transactions/{transactionId}" method="get" %}
[swagger_marketplace_1.0.5_UAT.yaml](../../.gitbook/assets/swagger_marketplace_1.0.5_UAT.yaml)
{% endswagger %}

### OrderSplits

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.5_UAT.yaml" path="/order-splits" method="post" %}
[swagger_marketplace_1.0.5_UAT.yaml](../../.gitbook/assets/swagger_marketplace_1.0.5_UAT.yaml)
{% endswagger %}

### Transferts

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.5_UAT.yaml" path="/transfers" method="post" %}
[swagger_marketplace_1.0.5_UAT.yaml](../../.gitbook/assets/swagger_marketplace_1.0.5_UAT.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.5_UAT.yaml" path="/transfers" method="get" %}
[swagger_marketplace_1.0.5_UAT.yaml](../../.gitbook/assets/swagger_marketplace_1.0.5_UAT.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.5_UAT.yaml" path="/transfers/{transferId}" method="get" %}
[swagger_marketplace_1.0.5_UAT.yaml](../../.gitbook/assets/swagger_marketplace_1.0.5_UAT.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.5_UAT.yaml" path="/transfers/{transferId}" method="delete" %}
[swagger_marketplace_1.0.5_UAT.yaml](../../.gitbook/assets/swagger_marketplace_1.0.5_UAT.yaml)
{% endswagger %}

### PayoutMerchants

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.5_UAT.yaml" path="/payout-merchants" method="post" %}
[swagger_marketplace_1.0.5_UAT.yaml](../../.gitbook/assets/swagger_marketplace_1.0.5_UAT.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.5_UAT.yaml" path="/payout-merchants" method="get" %}
[swagger_marketplace_1.0.5_UAT.yaml](../../.gitbook/assets/swagger_marketplace_1.0.5_UAT.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.5_UAT.yaml" path="/payout-merchants/{payoutMerchantId}" method="get" %}
[swagger_marketplace_1.0.5_UAT.yaml](../../.gitbook/assets/swagger_marketplace_1.0.5_UAT.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.5_UAT.yaml" path="/payout-merchants/{payoutMerchantId}" method="delete" %}
[swagger_marketplace_1.0.5_UAT.yaml](../../.gitbook/assets/swagger_marketplace_1.0.5_UAT.yaml)
{% endswagger %}

### PayoutSellers

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.5_UAT.yaml" path="/sellers/{sellerId}/payout-sellers" method="post" %}
[swagger_marketplace_1.0.5_UAT.yaml](../../.gitbook/assets/swagger_marketplace_1.0.5_UAT.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.5_UAT.yaml" path="/sellers/{sellerId}/payout-sellers" method="get" %}
[swagger_marketplace_1.0.5_UAT.yaml](../../.gitbook/assets/swagger_marketplace_1.0.5_UAT.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.5_UAT.yaml" path="/sellers/{sellerId}/payout-sellers/{payoutSellerId}" method="get" %}
[swagger_marketplace_1.0.5_UAT.yaml](../../.gitbook/assets/swagger_marketplace_1.0.5_UAT.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.5_UAT.yaml" path="/sellers/{sellerId}/payout-sellers/{payoutSellerId}" method="delete" %}
[swagger_marketplace_1.0.5_UAT.yaml](../../.gitbook/assets/swagger_marketplace_1.0.5_UAT.yaml)
{% endswagger %}

### PayoutSellerAmounts

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.5_UAT.yaml" path="/sellers/{sellerId}/payout-seller-amounts" method="post" %}
[swagger_marketplace_1.0.5_UAT.yaml](../../.gitbook/assets/swagger_marketplace_1.0.5_UAT.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.5_UAT.yaml" path="/sellers/{sellerId}/payout-seller-amounts" method="get" %}
[swagger_marketplace_1.0.5_UAT.yaml](../../.gitbook/assets/swagger_marketplace_1.0.5_UAT.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.5_UAT.yaml" path="/sellers/{sellerId}/payout-seller-amounts/{payoutSellerAmountId}" method="get" %}
[swagger_marketplace_1.0.5_UAT.yaml](../../.gitbook/assets/swagger_marketplace_1.0.5_UAT.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.5_UAT.yaml" path="/sellers/{sellerId}/payout-seller-amounts/{payoutSellerAmountId}" method="delete" %}
[swagger_marketplace_1.0.5_UAT.yaml](../../.gitbook/assets/swagger_marketplace_1.0.5_UAT.yaml)
{% endswagger %}

### Accounts

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.5_UAT.yaml" path="/accounts" method="get" %}
[swagger_marketplace_1.0.5_UAT.yaml](../../.gitbook/assets/swagger_marketplace_1.0.5_UAT.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.5_UAT.yaml" path="/sellers/{sellerId}/accounts" method="get" %}
[swagger_marketplace_1.0.5_UAT.yaml](../../.gitbook/assets/swagger_marketplace_1.0.5_UAT.yaml)
{% endswagger %}



Download OpenAPI specs:

{% file src="../../.gitbook/assets/swagger_marketplace_1.0.5_UAT.yaml" %}
YAML marketplace services for UAT
{% endfile %}
