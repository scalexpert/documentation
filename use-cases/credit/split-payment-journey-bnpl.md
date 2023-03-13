---
description: Run a split payment journey
---

# Split Payment Journey (BNPL)

## Run a Split Payment journey (BNPL[^1])

Run a Split Payment Journey (BNPL) is two steps process:

{% hint style="info" %}
As of today, Split payment e-financing solution is proposed by FRANFINANCE for France country only.
{% endhint %}

1. e-Financing Split Payment buyer journey (BNPL)\
   This step is executed by the producer (FRANFINANCE). This journey is a 2 screens payment experience: a-confirm identity of the buyer, b-proceed payment card (Payment is under responsibility of a PSP partner).\
   _<mark style="background-color:orange;">Mettre ici quelques images du parcours FF</mark>_\
   At the end of the split payment journey, the buyer will be redirected on the e-merchant confirmation e-website page.
2. Confirmation page on e-commerce website\
   After the redirection, the merchant will have to access the [`GET credit/v1/subscriptions/{creditSubscriptionId} API`](../../api-reference/credit-api.md#credit-v1-subscriptions-creditsubscriptionid) in order to get the resulting status. The status could be either ACCEPTED or REJECTED (cf. attribute field "consolidatedStatus"). Once received the confirmation page will be displayed to the buyer. If ACCEPTED the merchant can deliver the goods to the buyer.

<figure><img src="../../.gitbook/assets/Split payment journey .png" alt=""><figcaption></figcaption></figure>

[^1]: "Buy Now Pay Later"&#x20;
