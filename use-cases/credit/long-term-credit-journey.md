---
description: Run a Long Term Credit Journey
---

# Long Term Credit journey

## Run a Long Term Credit journey

Run a Long Term Credit Journey is three steps process:

{% hint style="info" %}
As of today, Long Term e-financing credit solutions are proposed by FRANFINANCE for France and by HANSEATIC BANK For Germany.
{% endhint %}

1. e-Financing Long Term Credit buyer journey (BNPL)\
   This step is executed by the producer (FRANFINANCE or HANSEATIC BANK). This journey is a few screens credit experience of which Buyer will complete its credit application before getting scoring from the bank.\
   _<mark style="background-color:orange;">Mettre ici quelques images du parcours FF</mark>_\
   At the end of the Long Term Credit journey, the buyer will be redirected on the e-merchant confirmation e-website page.
2. Confirmation page on e-commerce website\
   After the redirection, the merchant will have to access the [`GET credit/v1/subscriptions/{creditSubscriptionId} API`](../../api-reference/credit-api.md#credit-v1-subscriptions-creditsubscriptionid) in order to get the resulting status. The status could be either PRE-ACCEPTED or REJECTED (cf. attribute field "consolidatedStatus").&#x20;
3. KYC and e-signature journey\

4.
5.
6. Once received the confirmation page will be displayed to the buyer. If ACCEPTED the merchant can deliver the goods to the buyer.

<figure><img src="../../.gitbook/assets/Long Term Credit journey .png" alt=""><figcaption></figcaption></figure>
