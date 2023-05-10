---
description: Run a Long Term Credit Journey for German Buyer
---

# Long Term Credit Journey France

## Run a Long Term Credit Journey for French Buyers

Run a Long Term Credit Journey is four steps process:

{% hint style="info" %}
Long Term e-financing credit solution is proposed by FRANFINANCE subsidiary For France.
{% endhint %}

1. e-Financing Long Term Credit journey for French buyers \
   This step is executed by the producer (FRANFINANCE). This journey is a few screens credit experience of which the buyer will complete its credit application before getting a pre-acceptation from the bank.\

2. Confirmation page on e-commerce website\
   After pre-acceptation from the bank, the buyer will be redirected on the e-merchant confirmation e-website page. The merchant will have to access the [`GET credit/v1/subscriptions/{creditSubscriptionId} API`](../../api-reference/e-financing-api/v.1.0.md#credit-v1-subscriptions-creditsubscriptionid) in order to get the resulting status. The status could be either PRE-ACCEPTED or REJECTED (cf. attribute field "consolidatedStatus").&#x20;
3. When Status is PRE-ACCEPTED, the buyer will be redirected to the KYC and e-signature journey managed by a bank partner (WEBID).&#x20;
4. Since contract is signed, the bank will confirm final acceptation. On daily basis the merchant will have to access the [`GET credit/v1/subscriptions/{creditSubscriptionId} API`](../../api-reference/e-financing-api/v.1.0.md#credit-v1-subscriptions-creditsubscriptionid) in order to get the resulting status. The status could be either ACCEPTED or REJECTED. If ACCEPTED the merchant can deliver the goods to the buyer.

<figure><img src="../../.gitbook/assets/Long Term Credit journey France (1).png" alt=""><figcaption><p>LT credit France</p></figcaption></figure>
