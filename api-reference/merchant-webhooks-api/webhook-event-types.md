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

### Payload of an event type

You can find the documentation in the `API GET merchant-webhooks/api/v1/events` .

Here is an exemple of  a payload:

```json
{
  "totalEventCount": 158,
  "events": [
    {
      "timestamp": "2023-06-27T13:20:30.456Z",
      "id": "44f5060e-a89c-11ed-afa1-0242ac120002",
      "correlationId": "7d9670fe-a0cf-4073-afde-bdc61ca49f75",
      "eventTypeCode": "CREDIT",
      "eventCode": "CANCELLED",
      "data": {
        "eventTypeCode": "string",
        "eventCode": "string",
        "merchantGlobalOrderId": "string",
        "insuranceSubscriptionId": "string",
        "consolidatedStatus": "INITIALIZED"
      },
      "replayCount": 0,
      "status": "ERROR",
      "timestampOfLastDeliveryAttempt": "2023-06-27T13:20:30.456Z",
      "httpStatusCodeOfLastDeliveryAttempt": 500
    }
  ]
}
```

The "data" structure depends of "eventTypeCode"

[^1]: Solutions "e-Financing", "Insurance" ...
