---
description: Version 1.0.6 Latest (only for partners )
---

# UAT API for partners

### Description

**Marketplace Services**

* The Marketplace Services API is used to execute the payment process from order until the payout.
* It offers the ability to register orders, transactions and then apply order-splits, transfers and payouts.
* Once the order is registered, the marketplace associates the transactions with the order. Then, the marketplace allocates funds to each seller and charges fees through the order-splits endpoint.
* Finally, the marketplace can make payments to the seller's external account or to its own external account.
* The endpoint /transfers provides the ability for the Marketplace to move funds between the seller account and the Marketplace account or vice versa.

### API sequence diagram

```mermaid
sequenceDiagram
note over Merchant,API: Order registration
Merchant->>API: POST #47;orders
API-->> Merchant: order registrated
note over Merchant,API: Payment transaction
Merchant->>API: POST #47;transactions
API-->> Merchant: transactions registrated 
note over Merchant,API: Split orders
Merchant->>API: POST #47;order-splits
API->>PSP: GET #47;transactions
PSP-->>API: 
API->>BANK: POST #47;transferWallet
BANK-->>API: 
API-->> Merchant: orders split 
note over Merchant,API: transfers
Merchant->>API: POST #47;transferts
API-->> Merchant: transfers registrated
note over Merchant,API: Payout sellers
Merchant->>API: POST #47;payout-sellers
API->>BANK: GET #47;payoutSellers
BANK-->>API: 
API-->> Merchant: Payout sellers done! 
note over Merchant,API: Payout merchants
Merchant->>API: POST #47;payout-merchants
API->>BANK: GET #47;payoutMerchants
BANK-->>API: 
API-->> Merchant: Payout merchants done!    
note over Merchant,API: Notifications
BANK-->>API: Status change (webhook)
API-->> Merchant: status change (weebhook)! 
```

### Orders

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.6_UAT.yaml" path="/orders" method="post" %}
[swagger_marketplace_1.0.6_UAT.yaml](../../.gitbook/assets/swagger_marketplace_1.0.6_UAT.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.6_UAT.yaml" path="/orders" method="get" %}
[swagger_marketplace_1.0.6_UAT.yaml](../../.gitbook/assets/swagger_marketplace_1.0.6_UAT.yaml)
{% endswagger %}

### Transactions

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.6_UAT.yaml" path="/transactions" method="post" %}
[swagger_marketplace_1.0.6_UAT.yaml](../../.gitbook/assets/swagger_marketplace_1.0.6_UAT.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.6_UAT.yaml" path="/transactions" method="get" %}
[swagger_marketplace_1.0.6_UAT.yaml](../../.gitbook/assets/swagger_marketplace_1.0.6_UAT.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.6_UAT.yaml" path="/transactions/{transactionId}" method="get" %}
[swagger_marketplace_1.0.6_UAT.yaml](../../.gitbook/assets/swagger_marketplace_1.0.6_UAT.yaml)
{% endswagger %}

### OrderSplits

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.6_UAT.yaml" path="/order-splits" method="post" %}
[swagger_marketplace_1.0.6_UAT.yaml](../../.gitbook/assets/swagger_marketplace_1.0.6_UAT.yaml)
{% endswagger %}

### Transferts

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.6_UAT.yaml" path="/transfers" method="post" %}
[swagger_marketplace_1.0.6_UAT.yaml](../../.gitbook/assets/swagger_marketplace_1.0.6_UAT.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.6_UAT.yaml" path="/transfers" method="get" %}
[swagger_marketplace_1.0.6_UAT.yaml](../../.gitbook/assets/swagger_marketplace_1.0.6_UAT.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.6_UAT.yaml" path="/transfers/{transferId}" method="get" %}
[swagger_marketplace_1.0.6_UAT.yaml](../../.gitbook/assets/swagger_marketplace_1.0.6_UAT.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.6_UAT.yaml" path="/transfers/{transferId}" method="delete" %}
[swagger_marketplace_1.0.6_UAT.yaml](../../.gitbook/assets/swagger_marketplace_1.0.6_UAT.yaml)
{% endswagger %}

### PayoutMerchants

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.6_UAT.yaml" path="/payout-merchants" method="post" %}
[swagger_marketplace_1.0.6_UAT.yaml](../../.gitbook/assets/swagger_marketplace_1.0.6_UAT.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.6_UAT.yaml" path="/payout-merchants" method="get" %}
[swagger_marketplace_1.0.6_UAT.yaml](../../.gitbook/assets/swagger_marketplace_1.0.6_UAT.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.6_UAT.yaml" path="/payout-merchants/{payoutMerchantId}" method="get" %}
[swagger_marketplace_1.0.6_UAT.yaml](../../.gitbook/assets/swagger_marketplace_1.0.6_UAT.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.6_UAT.yaml" path="/payout-merchants/{payoutMerchantId}" method="delete" %}
[swagger_marketplace_1.0.6_UAT.yaml](../../.gitbook/assets/swagger_marketplace_1.0.6_UAT.yaml)
{% endswagger %}

### PayoutSellers

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.6_UAT.yaml" path="/sellers/{sellerId}/payout-sellers" method="post" %}
[swagger_marketplace_1.0.6_UAT.yaml](../../.gitbook/assets/swagger_marketplace_1.0.6_UAT.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.6_UAT.yaml" path="/sellers/{sellerId}/payout-sellers" method="get" %}
[swagger_marketplace_1.0.6_UAT.yaml](../../.gitbook/assets/swagger_marketplace_1.0.6_UAT.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.6_UAT.yaml" path="/sellers/{sellerId}/payout-sellers/{payoutSellerId}" method="get" %}
[swagger_marketplace_1.0.6_UAT.yaml](../../.gitbook/assets/swagger_marketplace_1.0.6_UAT.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.6_UAT.yaml" path="/sellers/{sellerId}/payout-sellers/{payoutSellerId}" method="delete" %}
[swagger_marketplace_1.0.6_UAT.yaml](../../.gitbook/assets/swagger_marketplace_1.0.6_UAT.yaml)
{% endswagger %}

### PayoutSellerAmounts

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.6_UAT.yaml" path="/sellers/{sellerId}/payout-seller-amounts" method="post" %}
[swagger_marketplace_1.0.6_UAT.yaml](../../.gitbook/assets/swagger_marketplace_1.0.6_UAT.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.6_UAT.yaml" path="/sellers/{sellerId}/payout-seller-amounts" method="get" %}
[swagger_marketplace_1.0.6_UAT.yaml](../../.gitbook/assets/swagger_marketplace_1.0.6_UAT.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.6_UAT.yaml" path="/sellers/{sellerId}/payout-seller-amounts/{payoutSellerAmountId}" method="get" %}
[swagger_marketplace_1.0.6_UAT.yaml](../../.gitbook/assets/swagger_marketplace_1.0.6_UAT.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.6_UAT.yaml" path="/sellers/{sellerId}/payout-seller-amounts/{payoutSellerAmountId}" method="delete" %}
[swagger_marketplace_1.0.6_UAT.yaml](../../.gitbook/assets/swagger_marketplace_1.0.6_UAT.yaml)
{% endswagger %}

### Accounts

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.6_UAT.yaml" path="/accounts" method="get" %}
[swagger_marketplace_1.0.6_UAT.yaml](../../.gitbook/assets/swagger_marketplace_1.0.6_UAT.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.6_UAT.yaml" path="/sellers/{sellerId}/accounts" method="get" %}
[swagger_marketplace_1.0.6_UAT.yaml](../../.gitbook/assets/swagger_marketplace_1.0.6_UAT.yaml)
{% endswagger %}



Download OpenAPI specs:

{% file src="../../.gitbook/assets/swagger_marketplace_1.0.6_UAT.yaml" %}
YAML marketplace services for UAT
{% endfile %}
