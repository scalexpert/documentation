---
description: Run a Long Term Credit Journey for German Buyer
---

# Long Term Credit Journey Germany

## Run a Long Term Credit Journey for German Buyers

Run a Long Term Credit Journey is a four steps process:

{% hint style="info" %}
Long Term e-financing credit solution is proposed by HANSEATIC BANK SG, our subsidiary for Germany.
{% endhint %}

1. **e-Financing Long Term Credit journey for German buyers** \
   This step is executed by the producer (HANSEATIC BANK). This journey is a few screens credit experience of which the buyer will complete its credit application before getting a pre-acceptation from the bank.\

2. **Confirmation page on e-commerce website**\
   After pre-acceptation from the bank, the buyer will be redirected on the e-merchant confirmation e-website page. The merchant will have to access the [`GET credit/v1/subscriptions/{creditSubscriptionId} API`](../../api-reference/e-financing-api/) in order to get the resulting status. The status could be either PRE-ACCEPTED or REJECTED (cf. attribute field "consolidatedStatus").&#x20;
3. When Status is PRE-ACCEPTED, the buyer will be redirected to the KYC and e-signature journey managed by a bank partner (WEBID).&#x20;
4. Since contract is signed, the bank will confirm final acceptation. On daily basis the merchant will have to access the [`GET credit/v1/subscriptions/{creditSubscriptionId} API`](../../api-reference/e-financing-api/) in order to get the resulting status. The status could be either ACCEPTED or REJECTED. If ACCEPTED the merchant can deliver the goods to the buyer.

<figure><img src="../../.gitbook/assets/Long Term Credit journey (Germany).png" alt=""><figcaption></figcaption></figure>

<details>

<summary>IBAN and KYC pin codes for testing purposes</summary>

Test IBAN [https://fr.iban.com/testibans](https://fr.iban.com/testibans)&#x20;

**KYC pin codes**:\
\- for successful KYC use 123456\
\- for unsuccessful KYC use 654321&#x20;

**Important:** you have to type in a real mobile number to receive the final SMS for signature

</details>
