---
description: Weebhook event types reference
---

# Webhook event types

### List of event types

The list of webhook event types must be retrieve with API `merchant-webhooks/api/v1/event-types`

{% hint style="info" %}
The list of webhook event types depends of the solutions[^1] you've subscribed.&#x20;
{% endhint %}

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

### Payload of an event types

You can find the documentation embedded in the `API GET merchant-webhooks/api/v1/events`.

You can parse the response depending the content of "eventTypeCode" ("SC\_SUBSCRIPTION",  "SC\_CANCEL\_REQUEST", "CI\_SUBSCRIPTION", HELLO\_WORLD" ...)

Here is an exemple of  a payload of event on e-Financing subscriptions object when status code is set to "PRE\_ACCEPTED" meaning the subscription is pending final back-office financial institution.

The status "OK" and "replayCount" null mean that event have been received with success.&#x20;

```json
{
  "totalEventCount": 158,
  "events": [
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
      },
      "replayCount": 0,
      "status": "OK",
      "timestampOfLastDeliveryAttempt": "2023-06-27T13:20:30.456Z",
      "httpStatusCodeOfLastDeliveryAttempt": 200
    }
  ]
}
```

The "data" structure depends of "eventTypeCode" attribute:

### Event types "SC\_SUBSCRIPTION"

Concern only the "[e-financing" solutions ](../../for-discovery/credit/#e-financing-solution-codes)and events related to [status of credit subscriptions](../../for-discovery/credit/e-financing-status-life-cycle.md#statuses-definition) .

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

Concern only the "[e-financing" solutions ](../../for-discovery/credit/#e-financing-solution-codes)and events related to cancellations requests status.

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

Concern only the ["insurance" solutions](../../for-discovery/insurance/#insurance-solutions-codes) and events related to [subscription status.](../../for-discovery/insurance/insurance-status-life-cycle.md#statuses-definition)

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
        merchant side (to test end-to-end connectivity)
```
{% endcode %}

[^1]: Solutions "e-Financing", "Insurance" ...
