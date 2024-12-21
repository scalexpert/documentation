---
description: Weebhook event types reference
---

# Webhook event types

## List of event types

The list of webhook event types must be retrieve with API `merchant-webhooks/api/v1/event-types`

{% hint style="info" %}
The list of webhook event types depends of the solutions[^1] you've subscribed.&#x20;
{% endhint %}

### Solution e-financing event types

2 event types:\
\- SC\_SUBSCRIPTION : all events related to a status change\
\- SC\_CANCEL\_REQUEST: all events related to a cancel request

<table><thead><tr><th width="229">eventTypes</th><th width="240">EventTypeCodes</th><th>Description</th></tr></thead><tbody><tr><td>SC_SUBSCRIPTION</td><td>SC_SUBSCRIPTION_INITIALIZED</td><td>occurs whenever a subscription is initialized </td></tr><tr><td></td><td>SC_SUBSCRIPTION_PRE_ACCEPTED</td><td>occurs whenever a subscription is pre-accepted</td></tr><tr><td></td><td>SC_SUBSCRIPTION_ACCEPTED</td><td>occurs whenever a subscription is accepted</td></tr><tr><td></td><td>SC_SUBSCRIPTION_REJECTED</td><td>occurs whenever a subscription is rejected</td></tr><tr><td></td><td>SC_SUBSCRIPTION_CANCELLED</td><td>occurs whenever a subscription is cancelled</td></tr><tr><td></td><td>SC_SUBSCRIPTION_ABORTED</td><td>occurs whenever a subscription is aborted</td></tr><tr><td>SC_CANCEL_REQUEST</td><td>SC_CANCEL_REQUEST_CANCELLATION_ACCEPTED</td><td>occurs whenever a full cancellation is  accepted</td></tr><tr><td></td><td>SC_CANCEL_REQUEST_CANCELLATION_REJECTED</td><td>occurs whenever a full cancellation is  rejected</td></tr><tr><td></td><td>SC_CANCEL_REQUEST_PARTIAL_CANCELLATION_ACCEPTED</td><td>occurs whenever a partial cancellation is  accepted</td></tr><tr><td></td><td>SC_CANCEL_REQUEST_PARTIAL_CANCELLATION_REJECTED</td><td>occurs whenever a partial cancellation is  rejected</td></tr></tbody></table>

### Solution insurance event types

1 event type:\
\- CI\_SUBSCRIPTION: all events related to status change

<table><thead><tr><th width="220">eventTypes</th><th width="197">eventTypeCodes</th><th>Description</th></tr></thead><tbody><tr><td>CI_SUBSCRIPTION</td><td>CI_SUBSCRIPTION_SUBSCRIBED</td><td>occurs whenever a subscription is subscribed</td></tr><tr><td></td><td>CI_SUBSCRIPTION_REJECTED</td><td>occurs whenever a subscription is rejected</td></tr><tr><td></td><td>CI_SUBSCRIPTION_CANCELLED</td><td>occurs whenever a subscription is cancelled</td></tr><tr><td></td><td>CI_SUBSCRIPTION_ABORTED</td><td>occurs whenever a subscription is aborted</td></tr></tbody></table>

<details>

<summary>Example of response of API merchant-webhooks/api/v1/event-types</summary>

{% code title="Response of API merchant-webhooks/api/v1/event-types" overflow="wrap" %}
```yaml
{

    "eventTypes": [

        {

            "eventTypeCode": "SC_SUBSCRIPTION",

            "description": "All status updates related to a credit subscription",

            "eventCodes": [

                {

                    "eventCode": "SC_SUBSCRIPTION_INITIALIZED",

                    "description": "Occurs whenever a credit subscription is initialized"

                },

                {

                    "eventCode": "SC_SUBSCRIPTION_PRE_ACCEPTED",

                    "description": "Occurs whenever a credit subscription is pre-accepted"

                },

                {

                    "eventCode": "SC_SUBSCRIPTION_ACCEPTED",

                    "description": "Occurs whenever a credit subscription is accepted"

                },

                {

                    "eventCode": "SC_SUBSCRIPTION_REJECTED",

                    "description": "Occurs whenever a credit subscription is rejected"

                },

                {

                    "eventCode": "SC_SUBSCRIPTION_CANCELLED",

                    "description": "Occurs whenever a credit subscription is cancelled"

                },

                {

                    "eventCode": "SC_SUBSCRIPTION_ABORTED",

                    "description": "Occurs whenever a credit subscription is aborted"

                }

            ]

        },

        {

            "eventTypeCode": "SC_CANCEL_REQUEST",

            "description": "All status updates related to a credit cancellation request (total or partial cancellation)",

            "eventCodes": [

                {

                    "eventCode": "SC_CANCEL_REQUEST_CANCELLATION_ACCEPTED",

                    "description": "Occurs whenever a credit total cancellation request is accepted"

                },

                {

                    "eventCode": "SC_CANCEL_REQUEST_CANCELLATION_REJECTED",

                    "description": "Occurs whenever a credit total cancellation request is rejected"

                },

                {

                    "eventCode": "SC_CANCEL_REQUEST_PARTIAL_CANCELLATION_ACCEPTED",

                    "description": "Occurs whenever a credit partial cancellation request is accepted"

                },

                {

                    "eventCode": "SC_CANCEL_REQUEST_PARTIAL_CANCELLATION_REJECTED",

                    "description": "Occurs whenever a credit partial cancellation request is rejected"

                }

            ]

        },

        {

            "eventTypeCode": "CI_SUBSCRIPTION",

            "description": "All status updates related to an insurance subscription",

            "eventCodes": [

                {

                    "eventCode": "CI_SUBSCRIPTION_SUBSCRIBED",

                    "description": "Occurs whenever an insurance is subscribed"

                },

                {

                    "eventCode": "CI_SUBSCRIPTION_REJECTED",

                    "description": "Occurs whenever an insurance is rejected"

                },

                {

                    "eventCode": "CI_SUBSCRIPTION_CANCELLED",

                    "description": "Occurs whenever an insurance is cancelled"

                },

                {

                    "eventCode": "CI_SUBSCRIPTION_ABORTED",

                    "description": "Occurs whenever an insurance is aborted"

                }

            ]

        }

    ]

}
```
{% endcode %}



</details>

### Solution Marketplace Services event types

MP types are related to Marketplace Services . all events related to status change

<table data-full-width="true"><thead><tr><th>eventTypes</th><th>eventTypeCodes</th><th>Description</th></tr></thead><tbody><tr><td>MP_SELLER_ONBOARDING</td><td>MP_IBAN_AVAILABLE_FOR_PAYMENT</td><td>occurs whenever the IBAN for the 1€ payment is available for seller</td></tr><tr><td>MP_SELLER_ONBOARDING</td><td>MP_KYC_IN_PROGRESS</td><td>occurs whenever the kyc assessment is ongoing for a seller</td></tr><tr><td>MP_SELLER_ONBOARDING</td><td>MP_KYC_VALIDATED</td><td>occurs whenever the kyc is approved for a seller</td></tr><tr><td>MP_SELLER_ONBOARDING</td><td>MP_KYC_REFUSED</td><td>occurs whenever the kyc is refused and needs corrections</td></tr></tbody></table>

### Payload of an event types

You can find the documentation embedded in the `API GET merchant-webhooks/api/v1/events`.

{% hint style="warning" %}
The "data" structure depends of "eventTypeCode" attribute. You can parse the response depending the content of "eventTypeCode" ("SC\_SUBSCRIPTION",  "SC\_CANCEL\_REQUEST", "CI\_SUBSCRIPTION", HELLO\_WORLD" ...)
{% endhint %}

Here is an exemple of  a payload of event on e-Financing subscriptions object when status code is set to "PRE\_ACCEPTED" meaning the subscription is pending final back-office financial institution.

```json
{
      "timestamp": "2023-06-27T13:20:30.456Z",
      "id": "44f5060e-a89c-11ed-afa1-0242ac120002",
      "correlationId": "7d9670fe-a0cf-4073-afde-bdc61ca49f75",
      "eventTypeCode": "SC_SUBSCRIPTION",
      "eventCode": "SC_SUBSCRIPTION_PRE_ACCEPTED",
      "data": {
        "eventTypeCode": "SC_SUBSCRIPTION",
        "eventCode": "SC_SUBSCRIPTION_PRE_ACCEPTED",
        "merchantGlobalOrderId": "MYORDER-12345",
        "financedAmount": 500.00,
        "consolidatedStatus": "PRE_ACCEPTED"
      }
}
```

### Event types "SC\_SUBSCRIPTION"

Concern only the "[e-financing" solutions ](../../solutions-reference/credit/#e-financing-solution-codes)and events related to [status of credit subscriptions](../../solutions-reference/credit/e-financing-status-life-cycle.md#statuses-definition) .

{% code title="Payload SC_SUBSCRIPTION" overflow="wrap" %}
```yaml
    ScSubscriptionPayload:
      required:
        - eventTypeCode
      type: object
      properties:
        eventTypeCode:
          type: string
        eventCode:
          type: string
        merchantGlobalOrderId:
          type: string
        financedAmount:
          type: number
          format: float
        consolidatedStatus:
          type: string
          description: Current status of the buyer (final customer) credit subscription
```
{% endcode %}

### Event types "SC\_CANCEL\_REQUEST"

Concern only the "[e-financing" solutions ](../../solutions-reference/credit/#e-financing-solution-codes)and events related to cancellations requests status.

{% code title="Payload SC_CANCEL_REQUEST" overflow="wrap" %}
```yaml
    ScCancelRequestPayload:
      required:
        - eventTypeCode
      type: object
      properties:
        eventTypeCode:
          type: string
        eventCode:
          type: string
        merchantGlobalOrderId:
          type: string
        cancelledAmount:
          type: number
          format: float
        financedAmount:
          type: number
          format: float
        consolidatedStatus:
          type: string
          description: Current status of the buyer (final customer) credit subscription
        cancellationStatus:
          type: string
          enum:
            - REQUEST_FOR_PARTIAL_CANCELLATION
            - REQUEST_FOR_CANCELLATION
            - CANCELLATION_ACCEPTED
            - CANCELLATION_REJECTED
            - PARTIAL_CANCELLATION_ACCEPTED
            - PARTIAL_CANCELLATION_REJECTED
```
{% endcode %}

### Event types "CI\_SUBSCRIPTION"

Concern only the ["insurance" solutions](../../solutions-reference/insurance/#insurance-solutions-codes) and events related to [subscription status.](../../solutions-reference/insurance/insurance-status-life-cycle.md#statuses-definition)

{% code title="Payload CI_SUBSCRIPTION" overflow="wrap" %}
```yaml
    CiSubscriptionPayload:
      required:
        - eventTypeCode
      type: object
      properties:
        eventTypeCode:
          type: string
        eventCode:
          type: string
        merchantGlobalOrderId:
          type: string
        insuranceSubscriptionId:
          type: string
        consolidatedStatus:
          type: string
          description: Current status of the buyer (final customer) insurance subscription
          enum:
            - INITIALIZED
            - SUBSCRIBED
            - ACTIVATED
            - CANCELLED
            - TERMINATED
            - ABORTED
            - REJECTED
```
{% endcode %}

### Event types "HELLO\_WORLD"

This event type is only for testing purpose to enable testing you merchant configuration.

{% code title="Payload HELLO_WORLD " overflow="wrap" %}
```yaml
    WebhookPayloadForHelloWorld:
      required:
        - eventTypeCode
        - helloWorldMessage
      type: object
      properties:
        eventTypeCode:
          type: string
        eventCode:
          type: string
        helloWorldMessage:
          type: string
          description: Hello World message
          example: Hello World !
      description: >-
        Payload of the HelloWorld event used to test the webhooks feature on the
        merchant side (to test end-to-end connec
```
{% endcode %}

[^1]: Solutions "e-Financing", "Insurance" ...
