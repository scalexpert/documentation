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
& contract validation,
waiting e-buyer 
additional information
end note
    PRE_ACCEPTED --> ACCEPTED
note right of ACCEPTED
accepted directly or,
waiting delivery or,
waiting funding
end note
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

### Detail of sub-statuses

| Status       | Sub-statuses                                                         | Comment                                                                                                                                                      |
| ------------ | -------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| INITIALIZED  | SUBSCRIPTION IN PROGRESS                                             | E-buyer initiate the subscription and is fulfilling its e-financing journey                                                                                  |
| PRE-ACCEPTED | SUBSCRIPTION PRE-APPROVED BY PRODUCER WAITING FOR CONTRACT SIGNATURE | E-buyer complete e-financing journey and get pre-approval from producer. Next step is contract signature.                                                    |
| PRE-ACCEPTED | CONTRACT SIGNED BY CUSTOMER                                          | Contract signed by e-buyer                                                                                                                                   |
| ACCEPTED     | SUBSCRIPTION APPROVED BY PRODUCER                                    | Producer accepted e-financing directly (split payment only)                                                                                                  |
| ACCEPTED     | WAITING FOR THE DELIVERY CONFIRMATION                                | Producer accepted e-financing. Next step is delivery to be confirmed by merchant (credit only).                                                              |
| ACCEPTED     | AWAITING PAYMENT TO MERCHANT                                         | Delivery has been confirmed by merchant and producer will fund the merchant (credit only).                                                                   |
| ACCEPTED     | PAYMENT HAS BEEN ISSUED TO MERCHANT                                  | E-financing has been funded (credit only).                                                                                                                   |
| REJECTED     | SUBSCRIPTION REJECTED BY PRODUCER                                    | Subscription has been rejected by producer (payment or credit rejected).                                                                                     |
| ABORTED      | ABORTED BY CUSTOMER                                                  | E-buyer aborted its e-financing journey or its session expired.                                                                                              |
| ABORTED      | ABORTED DUE TO TECHNICAL ISSUE                                       | A technical issue has been encountered during e-financing journey.                                                                                           |
| ABORTED      | EXPIRED                                                              | Subscription has been automatically aborted by producer because it has not changed since 3 months (this delay could depend on producer rules)                |
| CANCELLED    | CANCELLED BY CUSTOMER                                                | E-financing subscription has been cancelled by customer (withdrawal period) or by merchant on behalf of e-buyer (cancellation full ou partial of delivery).  |



```mermaid fullWidth="true"
---
title: E-financing subscription sub-status life cycle
---
stateDiagram-v2
    [*] --> SUBSCRIPTION_IN_PROGRESS

    SUBSCRIPTION_IN_PROGRESS --> ABORTED_DUE_TO_TECHNICAL_ISSUE
    SUBSCRIPTION_IN_PROGRESS --> ABORTED_BY_CUSTOMER
    SUBSCRIPTION_IN_PROGRESS --> EXPIRED
    SUBSCRIPTION_IN_PROGRESS --> PRE_APPROVED_BY_PRODUCER_WAITING_FOR_CONTRACT_SIGNATURE: credit only
    SUBSCRIPTION_IN_PROGRESS  --> SUBSCRIPTION_APPROVED_BY_PRODUCER: Split payment only
    SUBSCRIPTION_IN_PROGRESS  --> SUBSCRIPTION_REJECTED_BY_PRODUCER

    SUBSCRIPTION_APPROVED_BY_PRODUCER --> CANCEL_BY_CUSTOMER
    note right of CANCEL_BY_CUSTOMER
    Cancel by customer before financing
    withdrawal period or has not signed
    or on behalf by merchant (split payment only)
    end note

    PRE_APPROVED_BY_PRODUCER_WAITING_FOR_CONTRACT_SIGNATURE --> CONTRACT_SIGNED_BY_CUSTOMER
    PRE_APPROVED_BY_PRODUCER_WAITING_FOR_CONTRACT_SIGNATURE --> CANCEL_BY_CUSTOMER
    PRE_APPROVED_BY_PRODUCER_WAITING_FOR_CONTRACT_SIGNATURE --> EXPIRED

    CONTRACT_SIGNED_BY_CUSTOMER --> SUBSCRIPTION_REJECTED_BY_PRODUCER
    CONTRACT_SIGNED_BY_CUSTOMER --> WAITING_FOR_THE_DELIVERY_CONFIRMATION
    CONTRACT_SIGNED_BY_CUSTOMER --> CANCEL_BY_CUSTOMER
    

    WAITING_FOR_THE_DELIVERY_CONFIRMATION --> AWAITING_PAYMENT_TO_MERCHANT
    WAITING_FOR_THE_DELIVERY_CONFIRMATION --> CANCEL_BY_CUSTOMER

    AWAITING_PAYMENT_TO_MERCHANT  --> PAYMENT_HAVE_BEEN_ISSUED_TO_MERCHANT
    AWAITING_PAYMENT_TO_MERCHANT  --> CANCEL_BY_CUSTOMER

  
    ABORTED_DUE_TO_TECHNICAL_ISSUE --> [*]
    ABORTED_BY_CUSTOMER --> [*]
    EXPIRED --> [*]
    CANCEL_BY_CUSTOMER --> [*]
    SUBSCRIPTION_APPROVED_BY_PRODUCER --> [*]
    SUBSCRIPTION_REJECTED_BY_PRODUCER --> [*]
    PAYMENT_HAVE_BEEN_ISSUED_TO_MERCHANT --> [*]


```
