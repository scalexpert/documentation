---
description: Run a Long Term Credit Journey for German Buyer
---

# Long Term Credit journey Germany

## Run a Long Term Credit journey for German users

Run a Long Term Credit Journey is four steps process:

{% hint style="info" %}
As of today, Long Term e-financing credit solution is proposed by HANSEATIC BANK For Germany.
{% endhint %}

1. e-Financing Long Term Credit buyer journey\
   This step is executed by the producer (HANSEATIC BANK). This journey is a few screens credit experience of which Buyer will complete its credit application before getting scoring from the bank.\
   _<mark style="background-color:orange;">Mettre ici quelques images du parcours LT FF et HB</mark>_&#x20;
2. Confirmation page on e-commerce website\
   After the scoring from the bank, the buyer will be redirected on the e-merchant confirmation e-website page. The merchant will have to access the [`GET credit/v1/subscriptions/{creditSubscriptionId} API`](../../api-reference/credit-api.md#credit-v1-subscriptions-creditsubscriptionid) in order to get the resulting status. The status could be either PRE-ACCEPTED or REJECTED (cf. attribute field "consolidatedStatus").&#x20;
3. When Status is PRE-ACCEPTED, the buyer will be redirected to the KYC and e-signature journey managed by a bank partner.&#x20;
4. When statuts
5.
6. Once received the confirmation page will be displayed to the buyer. If ACCEPTED the merchant can deliver the goods to the buyer.

<figure><img src="../../.gitbook/assets/Long Term Credit journey  (1).png" alt=""><figcaption></figcaption></figure>
