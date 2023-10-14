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
* CANCELLED: subcription cancelled by financial institution&#x20;

### Status life cycle:

<div data-full-width="true">

<figure><img src="../../.gitbook/assets/E-financing subscription status life cycle.drawio.png" alt=""><figcaption><p>E-financing subscription status life cycle</p></figcaption></figure>

</div>

```mermaid
graph TD

  REQUESTED --> INITIALIZED
  INITIALIZED --> ABORTED
  INITIALIZED --> PRE-ACCEPTED
  PRE-ACCEPTED --> ACCEPTED
  PRE-ACCEPTED --> REJECTED
  INITIALIZED --> ACCEPTED
  INITIALIZED --> REJECTED

```
