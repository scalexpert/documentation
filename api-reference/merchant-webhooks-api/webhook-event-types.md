---
description: Weebhook event types reference
---

# Webhook event types

{% hint style="info" %}
The list of weebhook event types depends of the solutions[^1] you've subscribed.&#x20;
{% endhint %}

The list of webhook event types must be retrieve with API `merchant-weebhooks/api/v1/event-types`

<details>

<summary>Example of response of API merchant-weebhooks/api/v1/event-types</summary>

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

[^1]: Solutions "e-Financing", "Insurance" ...
