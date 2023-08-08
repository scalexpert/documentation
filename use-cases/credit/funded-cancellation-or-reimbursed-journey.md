---
description: Manage funded, cancelled events
---

# Funded, Cancellation journeys

### Funded of a subscription

<details>

<summary>Draft featured not yet available</summary>

Currently this feature "FUNDED" event status is not yet available.

The credit subscription is FUNDED to the Merchant by the Financial institution after confirmation of the delivery of goods.

The merchant will have to inform of the delivery of goods by API (Not yet available).

Thus, the merchant will be informed by an event and a the [status](e-financing-status-life-cycle.md) will be visible in its portal.&#x20;

* FUNDED = Merchant has been funded for financing. Buyer amortization plan or payments has started.

</details>

### Cancellation of a subscription

* A buyer/merchant want to cancel its order completely&#x20;
* A buyer/merchant want to cancel its order partially (

All these actions would be available with through an API. In addition the merchant will have the possibility to cancel  a subscription in its Merchant portal. \
The [status](e-financing-status-life-cycle.md) of the subscription will be updated to:

* ACCEPTED = Subscription and payment are partially cancelled. Amount to be financed is updated.&#x20;
* CANCELLED = Subscription and payment or amortization are completely  cancelled

{% hint style="info" %}
For long credit finance, cancellation in only possible after return of delivery of goods. Thus merchant must declare return of delivery by API (not yet available). &#x20;
{% endhint %}

All events (FUNDED, CANCELLED) could be pushed to the merchant by [webhook](broken-reference) mechanism.

{% hint style="warning" %}
Cancellation and Refund APIs will available soon and the merchant will have a feature in its merchant portal to trigger these actions on behalf of the buyer.&#x20;
{% endhint %}

