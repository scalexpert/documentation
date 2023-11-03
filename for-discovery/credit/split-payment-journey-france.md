---
description: Run a split payment journey
---

# Split Payment Journey France

## Run a Split Payment journey France

Run a Split Payment Journey for French Buyer is two steps process:

{% hint style="info" %}
Split payment e-financing solution is proposed by FRANFINANCE SG subsidiary for French Buyers.
{% endhint %}

1. e-Financing Split Payment for French buyer journey\
   This step is executed by the producer (FRANFINANCE). This journey is a 2 screens payment experience: confirm identity of the buyer, proceed payment card (Payment is under responsibility of a PSP partner).\
   \
   At the end of the split payment journey, the buyer will be redirected on the e-merchant confirmation e-website page.
2. Confirmation page on e-commerce website\
   After the redirection, the merchant will have to access the [`GET credit/v1/subscriptions/{creditSubscriptionId} API`](../../api-reference/e-financing-api/) in order to get the resulting status. The status could be either ACCEPTED or REJECTED (cf. attribute field "consolidatedStatus"). Once received the confirmation page will be displayed to the buyer. If ACCEPTED the merchant can deliver the goods to the buyer.

<figure><img src="../../.gitbook/assets/Split payment journey (BNPL).png" alt=""><figcaption></figcaption></figure>

<details>

<summary>Card bank numbers for testing purpose</summary>

* ACCEPTED (CB) - 5017 6791 1038 0400
* REFUSED (CB) - 5017 6791 1038 0900
* ACCEPTED (VISA) - 5017 6792 1000 0700
* REFUSED (VISA) - 5017 6792 1000 0200
* ACCEPTED (Mastercard) - 5017 6794 1000 0500
* REFUSED (Mastercard) - 5017 6794 1000 0000

</details>
