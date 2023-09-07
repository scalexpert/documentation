---
description: How to cancel a subscription for split payment
---

# Cancellation journey Split Payment

## Cancel a Split Payment journey France

Split payment cancellation is a simple journey.

1. Prerequisites\
   Your subscription must be at [**ACCEPTED** ](../e-financing-status-life-cycle.md)status and the date of cancellation must be not over 90 days.
2. Cancel your subscription\
   2 cases are possible:\
   \- cancel fully the subscription: cancelled amount equal initial financed amount. in that case resulting status would [**CANCELLED** ](../e-financing-status-life-cycle.md). \
   \- cancel partially the subscription: cancelled amount is lower financial amount. Status of subscription unchanged but financial amount is decreased by cancelled amount.&#x20;

{% hint style="warning" %}
You can only cancel partially a subscription once !
{% endhint %}

Cancel a subscription by calling [**API `POST /e-financing/api/v1/subscriptions{subscriptionId}/_cancel`**](../../../api-reference/e-financing-api/) **.**\


<div data-full-width="false">

<figure><img src="../../../.gitbook/assets/Cancel an e-financing subscrition (split payment only).png" alt=""><figcaption><p>Cancellation journey for Split Payment</p></figcaption></figure>

</div>
