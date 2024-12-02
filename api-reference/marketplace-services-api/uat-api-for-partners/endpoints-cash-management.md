# Endpoints cash management

## Orders

{% swagger src="../../../.gitbook/assets/swagger_marketplace_1.0.19.yaml" path="/v1/orders" method="post" %}
[swagger_marketplace_1.0.19.yaml](../../../.gitbook/assets/swagger_marketplace_1.0.19.yaml)
{% endswagger %}

{% swagger src="../../../.gitbook/assets/swagger_marketplace_1.0.19.yaml" path="/v1/orders/{orderId}" method="patch" %}
[swagger_marketplace_1.0.19.yaml](../../../.gitbook/assets/swagger_marketplace_1.0.19.yaml)
{% endswagger %}

{% swagger src="../../../.gitbook/assets/swagger_marketplace_1.0.19.yaml" path="/v1/orders" method="get" %}
[swagger_marketplace_1.0.19.yaml](../../../.gitbook/assets/swagger_marketplace_1.0.19.yaml)
{% endswagger %}

{% swagger src="../../../.gitbook/assets/swagger_marketplace_1.0.19.yaml" path="/v1/orders/{orderId}" method="delete" %}
[swagger_marketplace_1.0.19.yaml](../../../.gitbook/assets/swagger_marketplace_1.0.19.yaml)
{% endswagger %}

### OrderSplits

{% swagger src="../../../.gitbook/assets/swagger_marketplace_1.0.19.yaml" path="/v1/order-splits" method="post" %}
[swagger_marketplace_1.0.19.yaml](../../../.gitbook/assets/swagger_marketplace_1.0.19.yaml)
{% endswagger %}

### Transactions

{% swagger src="../../../.gitbook/assets/swagger_marketplace_1.0.19.yaml" path="/v1/transactions" method="post" %}
[swagger_marketplace_1.0.19.yaml](../../../.gitbook/assets/swagger_marketplace_1.0.19.yaml)
{% endswagger %}

{% swagger src="../../../.gitbook/assets/swagger_marketplace_1.0.19.yaml" path="/v1/transactions/{transactionId}" method="get" %}
[swagger_marketplace_1.0.19.yaml](../../../.gitbook/assets/swagger_marketplace_1.0.19.yaml)
{% endswagger %}

{% swagger src="../../../.gitbook/assets/swagger_marketplace_1.0.19.yaml" path="/v1/transactions" method="get" %}
[swagger_marketplace_1.0.19.yaml](../../../.gitbook/assets/swagger_marketplace_1.0.19.yaml)
{% endswagger %}

{% swagger src="../../../.gitbook/assets/swagger_marketplace_1.0.19.yaml" path="/v1/transactions/{transactionId}" method="patch" %}
[swagger_marketplace_1.0.19.yaml](../../../.gitbook/assets/swagger_marketplace_1.0.19.yaml)
{% endswagger %}

{% swagger src="../../../.gitbook/assets/swagger_marketplace_1.0.19.yaml" path="/v1/transactions/{transactionId}" method="delete" %}
[swagger_marketplace_1.0.19.yaml](../../../.gitbook/assets/swagger_marketplace_1.0.19.yaml)
{% endswagger %}

### Transferts

{% swagger src="../../../.gitbook/assets/swagger_marketplace_1.0.19.yaml" path="/v1/transfers" method="post" %}
[swagger_marketplace_1.0.19.yaml](../../../.gitbook/assets/swagger_marketplace_1.0.19.yaml)
{% endswagger %}

{% swagger src="../../../.gitbook/assets/swagger_marketplace_1.0.19.yaml" path="/v1/transfers" method="get" %}
[swagger_marketplace_1.0.19.yaml](../../../.gitbook/assets/swagger_marketplace_1.0.19.yaml)
{% endswagger %}

{% swagger src="../../../.gitbook/assets/swagger_marketplace_1.0.19.yaml" path="/v1/transfers/{transferId}" method="get" %}
[swagger_marketplace_1.0.19.yaml](../../../.gitbook/assets/swagger_marketplace_1.0.19.yaml)
{% endswagger %}

{% swagger src="../../../.gitbook/assets/swagger_marketplace_1.0.19.yaml" path="/v1/transfers/{transferId}" method="delete" %}
[swagger_marketplace_1.0.19.yaml](../../../.gitbook/assets/swagger_marketplace_1.0.19.yaml)
{% endswagger %}

### PayoutMerchants

{% swagger src="../../../.gitbook/assets/swagger_marketplace_1.0.19.yaml" path="/v1/payout-merchants" method="post" %}
[swagger_marketplace_1.0.19.yaml](../../../.gitbook/assets/swagger_marketplace_1.0.19.yaml)
{% endswagger %}

{% swagger src="../../../.gitbook/assets/swagger_marketplace_1.0.19.yaml" path="/v1/payout-merchants" method="get" %}
[swagger_marketplace_1.0.19.yaml](../../../.gitbook/assets/swagger_marketplace_1.0.19.yaml)
{% endswagger %}

{% swagger src="../../../.gitbook/assets/swagger_marketplace_1.0.19.yaml" path="/v1/payout-merchants/{payoutMerchantId}" method="get" %}
[swagger_marketplace_1.0.19.yaml](../../../.gitbook/assets/swagger_marketplace_1.0.19.yaml)
{% endswagger %}

{% swagger src="../../../.gitbook/assets/swagger_marketplace_1.0.19.yaml" path="/v1/payout-merchants/{payoutMerchantId}" method="delete" %}
[swagger_marketplace_1.0.19.yaml](../../../.gitbook/assets/swagger_marketplace_1.0.19.yaml)
{% endswagger %}

### PayoutSellers

{% swagger src="../../../.gitbook/assets/swagger_marketplace_1.0.19.yaml" path="/v1/sellers/{sellerId}/payout-sellers" method="post" %}
[swagger_marketplace_1.0.19.yaml](../../../.gitbook/assets/swagger_marketplace_1.0.19.yaml)
{% endswagger %}

{% swagger src="../../../.gitbook/assets/swagger_marketplace_1.0.19.yaml" path="/v1/sellers/{sellerId}/payout-sellers" method="get" %}
[swagger_marketplace_1.0.19.yaml](../../../.gitbook/assets/swagger_marketplace_1.0.19.yaml)
{% endswagger %}

{% swagger src="../../../.gitbook/assets/swagger_marketplace_1.0.19.yaml" path="/v1/sellers/{sellerId}/payout-sellers/{payoutSellerId}" method="get" %}
[swagger_marketplace_1.0.19.yaml](../../../.gitbook/assets/swagger_marketplace_1.0.19.yaml)
{% endswagger %}

{% swagger src="../../../.gitbook/assets/swagger_marketplace_1.0.19.yaml" path="/v1/sellers/{sellerId}/payout-sellers/{payoutSellerId}" method="delete" %}
[swagger_marketplace_1.0.19.yaml](../../../.gitbook/assets/swagger_marketplace_1.0.19.yaml)
{% endswagger %}

### PayoutSellerAmounts

{% swagger src="../../../.gitbook/assets/swagger_marketplace_1.0.19.yaml" path="/v1/sellers/{sellerId}/payout-seller-amounts" method="post" %}
[swagger_marketplace_1.0.19.yaml](../../../.gitbook/assets/swagger_marketplace_1.0.19.yaml)
{% endswagger %}

{% swagger src="../../../.gitbook/assets/swagger_marketplace_1.0.19.yaml" path="/v1/sellers/{sellerId}/payout-seller-amounts" method="get" %}
[swagger_marketplace_1.0.19.yaml](../../../.gitbook/assets/swagger_marketplace_1.0.19.yaml)
{% endswagger %}

{% swagger src="../../../.gitbook/assets/swagger_marketplace_1.0.19.yaml" path="/v1/sellers/{sellerId}/payout-seller-amounts/{payoutSellerAmountId}" method="get" %}
[swagger_marketplace_1.0.19.yaml](../../../.gitbook/assets/swagger_marketplace_1.0.19.yaml)
{% endswagger %}

{% swagger src="../../../.gitbook/assets/swagger_marketplace_1.0.19.yaml" path="/v1/sellers/{sellerId}/payout-seller-amounts/{payoutSellerAmountId}" method="delete" %}
[swagger_marketplace_1.0.19.yaml](../../../.gitbook/assets/swagger_marketplace_1.0.19.yaml)
{% endswagger %}

### Accounts

{% swagger src="../../../.gitbook/assets/swagger_marketplace_1.0.19.yaml" path="/v1/accounts" method="get" %}
[swagger_marketplace_1.0.19.yaml](../../../.gitbook/assets/swagger_marketplace_1.0.19.yaml)
{% endswagger %}

{% swagger src="../../../.gitbook/assets/swagger_marketplace_1.0.19.yaml" path="/v1/sellers/{sellerId}/accounts" method="get" %}
[swagger_marketplace_1.0.19.yaml](../../../.gitbook/assets/swagger_marketplace_1.0.19.yaml)
{% endswagger %}
