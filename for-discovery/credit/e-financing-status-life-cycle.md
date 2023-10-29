---
description: Status life cycle of a e-Financing subscription
---

# E-financing Status life cycle

### Statuses  definition:

* REQUESTED: Subscription requested to financial institution&#x20;
* INITIALIZED: Subscription has been initialized by financial institution
* PRE\_ACCEPTED: Subscription pre-accepted pending KYC, contrat signature and final acceptation by financial institution
* ACCEPTED: Subscription accepted by financial institution
* REJECTED: subscription rejected by financial institution
* ABORTED: subscription has been aborted due to technical incident or user abort
* CANCELLED: subscription cancelled by financial institution&#x20;

### Status life cycle:

```mermaid
---
title: E-financing subscription status life cycle
---
stateDiagram-v2 
    [*] --> REQUESTED
    REQUESTED --> INITIALIZED 
    INITIALIZED --> ABORTED: technical incident or user abort
    INITIALIZED --> PRE_ACCEPTED
note right of PRE_ACCEPTED
pending KYC, signature 
& contract validation
end note
    PRE_ACCEPTED --> ACCEPTED
    PRE_ACCEPTED --> REJECTED
    INITIALIZED --> ACCEPTED
    INITIALIZED --> REJECTED
    ACCEPTED --> ACCEPTED: partial cancellation
    ACCEPTED --> CANCELLED: full cancellation
    REJECTED --> [*]
    CANCELLED --> [*]
    ABORTED --> [*]

```
