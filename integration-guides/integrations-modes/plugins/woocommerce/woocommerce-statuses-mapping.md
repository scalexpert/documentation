---
description: How e-financing statuses are mapped with standard WooCommerce statuses
---

# 🆕 WooCommerce statuses mapping

### How e-financing map WooCommerce statuses

In WooCommerce, orders follow a standard lifecycle with predefined statuses. The Scalexpert plugin is designed [to synchronize these statuses with its own lifecycle.](woocommerce-statuses-mapping.md#e-financing-statuses-diagram-with-woocommerce-mapping) As a result, when the e-financing subscription status changes, it automatically updates to the corresponding WooCommerce status. Ensure the "pulling job" is enabled to allow

{% hint style="warning" %}
Note that not all WooCommerce statuses directly correspond to e-financing statuses. For example, the WooCommerce status "TERMINATED" is not mapped in e-financing. This status is used by merchants when an order is completed (fully paid and delivered), whereas e-financing only pertains to the payment or financing of
{% endhint %}

For more information read Guideline on WooCommerce documentation:

{% embed url="https://woocommerce.com/document/gestion-des-commandes/" %}
WooCommerce order status management
{% endembed %}

### e-financing statuses diagram with WooCommerce mapping

```mermaid
---
title: E-financing subscription and Woocommerce status mapping
---
stateDiagram-v2 
    [*] --> INITIALIZED 

    INITIALIZED --> ABORTED: technical incident or user abort
    INITIALIZED --> PRE_ACCEPTED: credit only
    INITIALIZED --> ACCEPTED: split payment only
    INITIALIZED --> REJECTED: split payment only
note right of INITIALIZED
ON HOLD
end note
    PRE_ACCEPTED --> ACCEPTED
    PRE_ACCEPTED --> REJECTED
    PRE_ACCEPTED --> CANCELLED: cancelled by e-buyer
note right of PRE_ACCEPTED
ON HOLD 
end note
    ACCEPTED --> ACCEPTED: partial cancellation
    ACCEPTED --> CANCELLED: full cancellation
note left of ACCEPTED
PROCESSING
end note
    REJECTED --> [*]
note right of REJECTED
FAILED
end note
    CANCELLED --> [*]
note right of CANCELLED
CANCELLED
end note
    ABORTED --> [*]
note right of ABORTED
FAILED
end note

```
