---
description: Status life cycle of a e-Financing subscription
---

# E-financing Status life cycle

### Statuses  definition:

* INITIALIZED: Subscription has been initialized by financial institution
* PRE\_ACCEPTED: Subscription pre-accepted pending KYC, contrat signature and final acceptation by financial institution
* ACCEPTED: Subscription accepted by financial institution
* REJECTED: subscription rejected by financial institution
* ABORTED: subscription has been aborted due to technical incident or user abort
* CANCELLED: subscription cancelled by financial institution or e-buyer&#x20;

### Status life cycle:

```mermaid
---
title: E-financing subscription status life cycle
---
stateDiagram-v2 
    [*] --> INITIALIZED
    INITIALIZED --> ABORTED: technical incident or user abort
    INITIALIZED --> PRE_ACCEPTED
note right of PRE_ACCEPTED
pending KYC, signature 
& contract validation
end note
    PRE_ACCEPTED --> ACCEPTED
    PRE_ACCEPTED --> REJECTED
    PRE_ACCEPTED --> CANCELLED: cancelled by e-buyer
    INITIALIZED --> ACCEPTED
    INITIALIZED --> REJECTED
    ACCEPTED --> ACCEPTED: partial cancellation
    ACCEPTED --> CANCELLED: full cancellation
    REJECTED --> [*]
    CANCELLED --> [*]
    ABORTED --> [*]

```
