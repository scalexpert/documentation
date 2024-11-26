---
description: Version 1.0.18 Latest (only for partners )
---

# UAT API for partners

## 1 - Sellers on boarding

### Description

Sellers on boarding is 7 steps completion:

1. Merchant registers sellers&#x20;
2. Merchant registers all sellers contacts
3. Merchant registers all merchant documents
4. Merchant registers all contacts documents
5. Merchant submit a seller for KYC validation when all information required is complete.
6. Merchant ask seller for IBAN verification
7. Bank will provide KYC result (OK, KO, INCOMPLETE)

### API sequence diagram

```mermaid
sequenceDiagram
note over Merchant,API: 1-Registers Seller
Merchant->>API: PUT #47;sellers#47;{merchantSellersId}
API-->> Merchant: sellers registrated!

note over Merchant,API: 2-Registers Seller Contacts
Merchant->>API: POST #47;sellers#47;{merchantSellersId}#47;contacts
API-->> Merchant: contacts registrated!
Merchant->>API: PATCH #47;sellers#47;{merchantSellersId}#47;contacts
API-->> Merchant: contacts modified!
Merchant->>API: DELETE #47;sellers#47;{merchantSellersId}#47;contacts
API-->> Merchant: contacts deleted!

note over Merchant,API: 3-Registers Merchant Documents
Merchant->>API: POST #47;sellers#47;{merchantSellersId}#47;contacts#47;{contactId}#47;documents
API-->> Merchant: documents merchant registrated!
Merchant->>API: DELETED #47;sellers#47;{merchantSellersId}#47;contacts#47;{contactId}#47;documents
API-->> Merchant: documents merchant deleted!

note over Merchant,API: 4-Registers Contact Documents
Merchant->>API: POST #47;sellers#47;{merchantSellersId}#47;documents
API-->> Merchant: documents contact registrated!
Merchant->>API: DELETE #47;sellers#47;{merchantSellersId}#47;documents
API-->> Merchant: documents contact deleted!

note over Merchant,API: At any get seller information
Merchant->>API: GET #47;sellers#47;{merchantSellersId}
API-->> Merchant: sellers information!

note over Merchant,BANK: 5-Submit Seller On boarding for KYC validation
Merchant->>API: POST #47;sellers#47;{merchantSellersId}#47;_assess-kyc
API->>BANK: ask the Bank to assess KYC
API-->> Merchant: KYC seller on going and waiting for IBAN verification notification
BANK->> API: provide IBAN seller
API-->> Merchant: IBAN notification (webhook)
Merchant->>API: GET #47;sellers#47;{merchantSellersId} retrieve IBAN
note over Merchant,Seller: 6-ask Seller for IBAN verification
Merchant->>Seller: provide IBAN
Seller->>BANK: execute 1€ tranfer 

note over Merchant,BANK: 7-BANK provide KYC result
BANK-->>API: 
API-->>Merchant: confirme KYC acceptation or rejection () 

note over Merchant,API: merchant would have repeating steps 2,3,4,5 if necessary

```

### Sellers Onboarding

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.18.yaml" path="/sellers/{merchantSellerId}" method="put" %}
[swagger_marketplace_1.0.18.yaml](../../.gitbook/assets/swagger_marketplace_1.0.18.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.18.yaml" path="/sellers/{merchantSellerId}/_assess-kyc" method="post" %}
[swagger_marketplace_1.0.18.yaml](../../.gitbook/assets/swagger_marketplace_1.0.18.yaml)
{% endswagger %}

### Contacts

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.18.yaml" path="/sellers/{merchantSellerId}/contacts" method="post" %}
[swagger_marketplace_1.0.18.yaml](../../.gitbook/assets/swagger_marketplace_1.0.18.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.18.yaml" path="/sellers/{merchantSellerId}/contacts/{contactId}" method="delete" %}
[swagger_marketplace_1.0.18.yaml](../../.gitbook/assets/swagger_marketplace_1.0.18.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.18.yaml" path="/sellers/{merchantSellerId}/contacts/{contactId}" method="patch" %}
[swagger_marketplace_1.0.18.yaml](../../.gitbook/assets/swagger_marketplace_1.0.18.yaml)
{% endswagger %}

### Documents

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.18.yaml" path="/sellers/{merchantSellerId}/documents" method="post" %}
[swagger_marketplace_1.0.18.yaml](../../.gitbook/assets/swagger_marketplace_1.0.18.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.18.yaml" path="/sellers/{merchantSellerId}/contacts/{contactId}/documents" method="post" %}
[swagger_marketplace_1.0.18.yaml](../../.gitbook/assets/swagger_marketplace_1.0.18.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.18.yaml" path="/sellers/{merchantSellerId}/documents/{documentId}" method="delete" %}
[swagger_marketplace_1.0.18.yaml](../../.gitbook/assets/swagger_marketplace_1.0.18.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.18.yaml" path="/sellers/{merchantSellerId}/contacts/{contactId}/documents/{documentId}" method="delete" %}
[swagger_marketplace_1.0.18.yaml](../../.gitbook/assets/swagger_marketplace_1.0.18.yaml)
{% endswagger %}

### Sellers

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.18.yaml" path="/sellers/{merchantSellerId}" method="get" %}
[swagger_marketplace_1.0.18.yaml](../../.gitbook/assets/swagger_marketplace_1.0.18.yaml)
{% endswagger %}



## 2- Cash management

### **Description**

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
API-->> Merchant: order registrated!
note over Merchant,API: Payment transaction
Merchant->>API: POST #47;transactions
API-->> Merchant: transactions registrated! 
note over Merchant,API: Split orders
Merchant->>API: POST #47;order-splits
API->>PSP: GET #47;transactions
PSP-->>API: 
API->>BANK: POST #47;transferWallet
BANK-->>API: 
API-->> Merchant: orders split done! 
note over Merchant,API: transfers
Merchant->>API: POST #47;transferts
API-->> Merchant: transfers done!
note over Merchant,API: Payout sellers
Merchant->>API: POST #47;sellers#47;{sellerId}#47;payout-sellers
API->>BANK: POST #47;payoutSellers
BANK-->>API: 
API-->> Merchant: Payout sellers done! 
note over Merchant,API: Payout merchants
Merchant->>API: POST #47;payout-merchants
API->>BANK: POST #47;payoutMerchants
BANK-->>API: 
API-->> Merchant: Payout merchants done!    
note over Merchant,API: Notifications
BANK-->>API: Status change (webhook)
API-->> Merchant: status change (weebhook)! 
```

## Orders

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.18.yaml" path="/orders" method="post" %}
[swagger_marketplace_1.0.18.yaml](../../.gitbook/assets/swagger_marketplace_1.0.18.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.18.yaml" path="/orders/{orderId}" method="patch" %}
[swagger_marketplace_1.0.18.yaml](../../.gitbook/assets/swagger_marketplace_1.0.18.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.18.yaml" path="/orders" method="get" %}
[swagger_marketplace_1.0.18.yaml](../../.gitbook/assets/swagger_marketplace_1.0.18.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.18.yaml" path="/orders/{orderId}" method="delete" %}
[swagger_marketplace_1.0.18.yaml](../../.gitbook/assets/swagger_marketplace_1.0.18.yaml)
{% endswagger %}

### OrderSplits

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.18.yaml" path="/order-splits" method="post" %}
[swagger_marketplace_1.0.18.yaml](../../.gitbook/assets/swagger_marketplace_1.0.18.yaml)
{% endswagger %}

### Transactions

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.18.yaml" path="/transactions" method="post" %}
[swagger_marketplace_1.0.18.yaml](../../.gitbook/assets/swagger_marketplace_1.0.18.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.18.yaml" path="/transactions" method="get" %}
[swagger_marketplace_1.0.18.yaml](../../.gitbook/assets/swagger_marketplace_1.0.18.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.18.yaml" path="/transactions/{transactionId}" method="get" %}
[swagger_marketplace_1.0.18.yaml](../../.gitbook/assets/swagger_marketplace_1.0.18.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.18.yaml" path="/transactions/{transactionId}" method="patch" %}
[swagger_marketplace_1.0.18.yaml](../../.gitbook/assets/swagger_marketplace_1.0.18.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.18.yaml" path="/transactions/{transactionId}" method="delete" %}
[swagger_marketplace_1.0.18.yaml](../../.gitbook/assets/swagger_marketplace_1.0.18.yaml)
{% endswagger %}

### Transferts

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.18.yaml" path="/transfers" method="post" %}
[swagger_marketplace_1.0.18.yaml](../../.gitbook/assets/swagger_marketplace_1.0.18.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.18.yaml" path="/transfers" method="get" %}
[swagger_marketplace_1.0.18.yaml](../../.gitbook/assets/swagger_marketplace_1.0.18.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.18.yaml" path="/transfers/{transferId}" method="get" %}
[swagger_marketplace_1.0.18.yaml](../../.gitbook/assets/swagger_marketplace_1.0.18.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.18.yaml" path="/transfers/{transferId}" method="delete" %}
[swagger_marketplace_1.0.18.yaml](../../.gitbook/assets/swagger_marketplace_1.0.18.yaml)
{% endswagger %}

### PayoutMerchants

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.18.yaml" path="/payout-merchants" method="post" %}
[swagger_marketplace_1.0.18.yaml](../../.gitbook/assets/swagger_marketplace_1.0.18.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.18.yaml" path="/payout-merchants" method="get" %}
[swagger_marketplace_1.0.18.yaml](../../.gitbook/assets/swagger_marketplace_1.0.18.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.18.yaml" path="/payout-merchants/{payoutMerchantId}" method="get" %}
[swagger_marketplace_1.0.18.yaml](../../.gitbook/assets/swagger_marketplace_1.0.18.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.18.yaml" path="/payout-merchants/{payoutMerchantId}" method="delete" %}
[swagger_marketplace_1.0.18.yaml](../../.gitbook/assets/swagger_marketplace_1.0.18.yaml)
{% endswagger %}

### PayoutSellers

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.18.yaml" path="/sellers/{sellerId}/payout-sellers" method="post" %}
[swagger_marketplace_1.0.18.yaml](../../.gitbook/assets/swagger_marketplace_1.0.18.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.18.yaml" path="/sellers/{sellerId}/payout-sellers" method="get" %}
[swagger_marketplace_1.0.18.yaml](../../.gitbook/assets/swagger_marketplace_1.0.18.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.18.yaml" path="/sellers/{sellerId}/payout-sellers/{payoutSellerId}" method="get" %}
[swagger_marketplace_1.0.18.yaml](../../.gitbook/assets/swagger_marketplace_1.0.18.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.18.yaml" path="/sellers/{sellerId}/payout-sellers/{payoutSellerId}" method="delete" %}
[swagger_marketplace_1.0.18.yaml](../../.gitbook/assets/swagger_marketplace_1.0.18.yaml)
{% endswagger %}

### PayoutSellerAmounts

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.18.yaml" path="/sellers/{sellerId}/payout-seller-amounts/{payoutSellerAmountId}" method="delete" %}
[swagger_marketplace_1.0.18.yaml](../../.gitbook/assets/swagger_marketplace_1.0.18.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.18.yaml" path="/sellers/{sellerId}/payout-seller-amounts/{payoutSellerAmountId}" method="get" %}
[swagger_marketplace_1.0.18.yaml](../../.gitbook/assets/swagger_marketplace_1.0.18.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.18.yaml" path="/sellers/{sellerId}/payout-seller-amounts" method="post" %}
[swagger_marketplace_1.0.18.yaml](../../.gitbook/assets/swagger_marketplace_1.0.18.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.18.yaml" path="/sellers/{sellerId}/payout-seller-amounts" method="get" %}
[swagger_marketplace_1.0.18.yaml](../../.gitbook/assets/swagger_marketplace_1.0.18.yaml)
{% endswagger %}

### Accounts

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.18.yaml" path="/accounts" method="get" %}
[swagger_marketplace_1.0.18.yaml](../../.gitbook/assets/swagger_marketplace_1.0.18.yaml)
{% endswagger %}

{% swagger src="../../.gitbook/assets/swagger_marketplace_1.0.18.yaml" path="/sellers/{sellerId}/accounts" method="get" %}
[swagger_marketplace_1.0.18.yaml](../../.gitbook/assets/swagger_marketplace_1.0.18.yaml)
{% endswagger %}



Download OpenAPI specs:

{% file src="../../.gitbook/assets/swagger_marketplace_1.0.18.yaml" %}
YAML marketplace services for UAT
{% endfile %}
