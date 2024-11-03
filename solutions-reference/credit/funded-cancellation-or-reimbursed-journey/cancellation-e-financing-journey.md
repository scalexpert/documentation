---
description: How to cancel a e-financing subscription
---

# Cancellation e-financing journey

## Cancel an e-financing subscription

Cancellation is a simple journey.

1.  Prerequisites

    1. Split payment\
       Your subscription must be at [**ACCEPTED** ](../e-financing-status-life-cycle.md)status and the date of cancellation must be not over 90 days.
    2. long credit\
       You can cancel your subscription till your withdrawal period has not expired.&#x20;

    All cases  cancellation are described [here.](../e-financing-status-life-cycle.md#detail-of-sub-statuses)
2. Cancel your subscription\
   2 cases are possible:\
   \- cancel fully the subscription: cancelled amount equal initial financed amount. in that case resulting status will be [**CANCELLED** ](../e-financing-status-life-cycle.md). \
   \- cancel partially the subscription: cancelled amount is lower financial amount. Status of subscription is unchanged **(**[**ACCEPTED**](../e-financing-status-life-cycle.md)**)** but financial amount is decreased by cancelled amount.&#x20;

{% hint style="warning" %}
You can only cancel partially a subscription once !
{% endhint %}

### Cancel via API (split payment only)

{% hint style="warning" %}
For now, cancellation via API is only available for split payment. For long credit, please contact FRANFINANCE producer directly.
{% endhint %}

Cancel a subscription by calling API `POST /e-`[`financing/api/v1/subscriptions{subscriptionId}/_cancel`](../../../api-reference/e-financing-api/) (only available for split payment).

<div data-full-width="false">

<figure><img src="../../../.gitbook/assets/Cancel an e-financing subscrition (split payment only).png" alt=""><figcaption><p>Cancellation journey for Split Payment</p></figcaption></figure>

</div>
