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
   This step is executed by the producer (FRANFINANCE). This journey consist of a few screens credit experience of which the buyer will complete its credit application including KYC and contract signature before getting a pre-acceptation from the bank.&#x20;
2. Confirmation page on e-commerce website\
   After pre-acceptation from the bank, the buyer will be redirected on the e-merchant confirmation e-website page. The merchant will have to access the [`GET credit/v1/subscriptions/{creditSubscriptionId} API`](../../api-reference/e-financing-api/) in order to get the status. The status could be either PRE-ACCEPTED or REJECTED (cf.  [status life cycle](e-financing-status-life-cycle.md)).&#x20;
3. Since contract is signed, the bank will confirm final acceptation. On daily basis the merchant will have to access with [`GET credit/v1/subscriptions/{creditSubscriptionId} API`](../../api-reference/e-financing-api/) in order to get the final status. The status could be either ACCEPTED or REJECTED. If ACCEPTED the merchant can deliver the goods to the buyer.

<figure><img src="../../.gitbook/assets/Long Term Credit journey (France).png" alt=""><figcaption><p>LT credit France</p></figcaption></figure>

<details>

<summary>IBAN  codes for testing purposes</summary>

Test IBAN [https://fr.iban.com/testibans](https://fr.iban.com/testibans)&#x20;

**Important** Follow the "happy path" to complete your tests:\
\- use real identity documents to complet the KYC step\
\- Finance lower than 3000 € will be automatically accepted\
For any other cases contact our integration support team [sg-ecommerce-support.world@socgen.com](mailto://sg-ecommerce-support.world@socgen.com)&#x20;

</details>
