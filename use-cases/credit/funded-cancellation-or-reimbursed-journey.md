---
description: Follow cancellation, funded or refund events
---

# Funded, Cancellation or Reimbursed journey

The Financing (credit or payment) is considered as stated accordingly the general conditions of the solution. Thus, the merchant will be informed by an events and a specific [status](../../generic-objects-and-codes/status-codes.md) FUNDED and this status will be visible in its portal.&#x20;

But other events could occurs before or after funding:

* A buyer want to cancel its order completely or partially
* A merchant want to cancel the order completely or partially

In both cases, this will trigger an action that would be available with a dedicated endpoint. In addition the merchant will have the possibility to cancel or refund a subscription in its Merchant portal. \
The [status](../../generic-objects-and-codes/status-codes.md) of the subscription will be updated to CANCELLED or REIMBURSED (REFUND):

* CANCELLED = Subscription is completely cancelled
* REIMBURSED = Subscription is partially cancelled and a partial reimbursement have been done.

All events could be push to the merchant by [webhook](broken-reference) mechanism.

{% hint style="warning" %}
Cancellation and Refund APIs will available soon and the merchant will have a feature in its merchant portal to trigger these actions on behalf of the buyer.&#x20;
{% endhint %}

