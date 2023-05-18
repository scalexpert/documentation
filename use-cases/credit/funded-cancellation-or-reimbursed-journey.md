---
description: Manage cancellation, funded or refund events
---

# Funded, Cancellation or Reimbursed journey

The Financing journey (credit or payment) is considered as FUNDED accordingly the general conditions of the solution. Thus, the merchant will be informed by an events and a the [status](status-life-cycle.md) will be visible in its portal.&#x20;

* FUNDED = Buyer amortization plan or payments has started.

But other events could occurs before or after funding:

* A buyer want to cancel its order completely or partially
* A merchant want to cancel the order completely or partially

All these actions would be available with through an API. In addition the merchant will have the possibility to cancel or refund a subscription in its Merchant portal. \
The [status](status-life-cycle.md) of the subscription will be updated to CANCELLED or REIMBURSED (REFUND):

* CANCELLED = Subscription and payment or amortization are completely cancelled
* REIMBURSED = Subscription and payment or amortization are partially cancelled and a partial reimbursement have been done.

All events (FUNDED, CANCELLED, REIMBURSED) could be pushed to the merchant by [webhook](broken-reference) mechanism.

{% hint style="warning" %}
Cancellation and Refund APIs will available soon and the merchant will have a feature in its merchant portal to trigger these actions on behalf of the buyer.&#x20;
{% endhint %}

