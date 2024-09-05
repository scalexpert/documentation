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
| PRE-ACCEPTED | WAITING CUSTOMER FOR ADDITIONAL INFORMATION                          | Contract pending waiting for e-buyer additional information                                                                                                  |
| ACCEPTED     | SUBSCRIPTION APPROVED BY PRODUCER                                    | Producer accepted e-financing directly (split payment only)                                                                                                  |
| ACCEPTED     | WAITING FOR THE DELIVERY CONFIRMATION                                | Producer accepted e-financing. Next step is delivery to be confirmed by merchant (credit only).                                                              |
| ACCEPTED     | AWAITING PAYMENT TO MERCHANT                                         | Delivery has been confirmed by merchant and producer will fund the merchant (credit only).                                                                   |
| ACCEPTED     | PAYMENT HAS BEEN ISSUED TO MERCHANT                                  | E-financing has been funded (credit only).                                                                                                                   |
| REJECTED     | SUBSCRIPTION REJECTED BY PRODUCER                                    | Subscription has been rejected by producer (payment or credit rejected).                                                                                     |
| ABORTED      | ABORTED BY CUSTOMER                                                  | E-buyer aborted its e-financing journey or its session expired.                                                                                              |
| ABORTED      | ABORTED DUE TO TECHNICAL ISSUE                                       | A technical issue has been encountered during e-financing journey.                                                                                           |
| CANCELLED    | CANCELLED BY CUSTOMER                                                | E-financing subscription has been cancelled by customer (withdrawal period) or by merchant on behalf of e-buyer (cancellation full ou partial of delivery).  |



```mermaid fullWidth="true"
---
title: E-financing subscription sub-status life cycle
---
stateDiagram-v2
    [*] --> SUBSCRIPTION_IN_PROGRESS

    SUBSCRIPTION_IN_PROGRESS --> ABORTED_DUE_TO_TECHNICAL_ISSUE: technical incident
    SUBSCRIPTION_IN_PROGRESS --> ABORTED_BY_CUSTOMER: aborted by customer
    SUBSCRIPTION_IN_PROGRESS --> PRE_ACCEPTED_WAITING_FOR_CONTRACT_SIGNATURE: credit only
    SUBSCRIPTION_IN_PROGRESS  --> SUBSCRIPTION_APPROVED_BY_PRODUCER: Split payment only
    SUBSCRIPTION_IN_PROGRESS  --> SUBSCRIPTION_REJECTED_BY_PRODUCER

    SUBSCRIPTION_APPROVED_BY_PRODUCER --> CANCEL_BY_CUSTOMER
    note right of CANCEL_BY_CUSTOMER
    Cancel by customer (withdrawal period) 
    or on behalf by merchant
    end note

    PRE_ACCEPTED_WAITING_FOR_CONTRACT_SIGNATURE --> CONTRACT_SIGNED_BY_CUSTOMER
    PRE_ACCEPTED_WAITING_FOR_CONTRACT_SIGNATURE --> SUBSCRIPTION_REJECTED_BY_PRODUCER
    PRE_ACCEPTED_WAITING_FOR_CONTRACT_SIGNATURE --> WAITING_CUSTOMER_FOR_ADDITIONAL_INFORMATION
    PRE_ACCEPTED_WAITING_FOR_CONTRACT_SIGNATURE --> CANCEL_BY_CUSTOMER

    WAITING_CUSTOMER_FOR_ADDITIONAL_INFORMATION --> CONTRACT_SIGNED_BY_CUSTOMER
    WAITING_CUSTOMER_FOR_ADDITIONAL_INFORMATION --> SUBSCRIPTION_REJECTED_BY_PRODUCER
    

    CONTRACT_SIGNED_BY_CUSTOMER --> WAITING_FOR_THE_DELIVERY_CONFIRMATION: credit only
    WAITING_FOR_THE_DELIVERY_CONFIRMATION --> AWAITING_PAYMENT_TO_MERCHANT
    AWAITING_PAYMENT_TO_MERCHANT  --> PAYMENT_HAVE_BEEN_ISSUED_TO_MERCHANT

    ABORTED_DUE_TO_TECHNICAL_ISSUE --> [*]
    ABORTED_BY_CUSTOMER --> [*]
    CANCEL_BY_CUSTOMER --> [*]
    PAYMENT_HAVE_BEEN_ISSUED_TO_MERCHANT --> [*]
    SUBSCRIPTION_REJECTED_BY_PRODUCER --> [*]

```
