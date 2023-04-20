---
description: Run a cancellation or refund journey by the buyer or by the merchant
---

# Cancellation or Reimbursed Journey

They could different uses cases that could issued a cancellation or a refund:

* A buyer want to cancel its order completely or partially
* A merchant want to cancel the order completely or partially

In both cases, this will trigger an action that would be available with a dedicated endpoint. \
In addition the merchant will have the possibility to cancel or refund a subscription in its Merchant portal. \
The [status](../../generic-objects-and-codes/status-codes.md) of the subscription will be updated to CANCELLED or REIMBURSED:

* CANCELLED = Subscription is completely cancelled
* REIMBURSED = Subscription is partially cancelled and a partial reimbursement have been done.

{% hint style="warning" %}
Cancellation and Refund APIs will available soon and the merchant will have a feature in its merchant portal to trigger these actions on behalf of the buyer.&#x20;
{% endhint %}

