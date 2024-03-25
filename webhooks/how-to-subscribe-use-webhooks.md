---
description: Merchant webhooks tutorial (Work in progress)
---

# 🚧 How to subscribe, use Webhooks

{% hint style="info" %}
Merchant Webhooks has just been released! :tada:  Pulling method stay another alternative but we recommend using webhooks instead. &#x20;
{% endhint %}

## How to subscribe to Merchant webhooks

There 2 ways to do it:\
\- through your merchant portal app\
\- though APIs

## 1-Subscribe through merchant portal app

Connect  your merchant portal app and start the Webhooks configuration on the dedicated tab of your personal information page.&#x20;

<figure><img src="../.gitbook/assets/Capture d’écran du 2024-03-06 16-55-02 (1).png" alt=""><figcaption><p>Start configuring webhooks</p></figcaption></figure>

### Add a new webhook endpoint

You can add a new webhook endpoint by clicking "start" or "add a new endpoint".

<figure><img src="../.gitbook/assets/Capture d’écran du 2024-03-21 14-28-02.png" alt="" width="325"><figcaption><p>Start entering a new webhook endpoint</p></figcaption></figure>

#### Configure your endpoint with security fields &#x20;

Mandatory fields <mark style="color:red;">\*</mark>

* Endpoint URL <mark style="color:red;">\*</mark>: name of URL endpoint that will be callback when a event subscribed occurs.
* Authentication method <mark style="color:red;">\*</mark>: choose among the authentication method available \[None | Basic auth | API key]

Fields to complete according authentication method:

| None                                      | Basic auth                                          | API key                                             |
| ----------------------------------------- | --------------------------------------------------- | --------------------------------------------------- |
| Secret <mark style="color:red;">\*</mark> | Identifier/login <mark style="color:red;">\*</mark> | Secret (API key) <mark style="color:red;">\*</mark> |
| Signature key                             | Password <mark style="color:red;">\*</mark>         | Signature key                                       |
|                                           | Signature key                                       |                                                     |
|                                           |                                                     |                                                     |

Identifier/login and password fields are required for basic auth only.

Secret is required for authentication None or API key. Secret is a string shared between you and scalexpert.&#x20;

Signature key is optional field for signing events with header X-BAAS-SIGNATURE. This add more security if needed.

{% hint style="warning" %}
When signature is used you would have to verify the signature before consuming event. See dedicated chapter "Verify signature of webhook event"  &#x20;
{% endhint %}

#### Configure your endpoint to listen events

Chose [events types](../api-reference/merchant-webhooks-api/webhook-event-types.md) to listen on the endpoint webhook url. Events types listed are the ones available for you that fit your solutions subscribed.

{% hint style="info" %}
You can listen multiple events types on the same endpoint. But we recommend subscribing separated endpoints because it will be easier to parse the payload according event type structure. see more details on event types [there](../api-reference/merchant-webhooks-api/webhook-event-types.md).&#x20;
{% endhint %}

### Manage webhooks endpoints

Once webhooks added, you van manage your webhooks endpoints at the webhooks tab. Manage webhooks allow you to change the configuration, activate/deactivate events.&#x20;

{% hint style="info" %}
You can activate/deactivate webhooks at any time for all events subscribed or events by events.&#x20;
{% endhint %}

<figure><img src="../.gitbook/assets/Capture d’écran du 2024-03-21 15-23-41.png" alt=""><figcaption><p>Manage webhooks endpoints</p></figcaption></figure>

### Test your webhooks configuration

We have added a special event type "HELLO\_WORLD" to allow you testing your webhooks url configuration.&#x20;

{% hint style="warning" %}
For now this feature is only available through API. if you want us to release it on merchant portal let us know [support](../support/how-to-contact-us.md) :e-mail:
{% endhint %}

### Retrieve events&#x20;

You can retrieve all events received and get details though [merchant-webhooks API](../api-reference/merchant-webhooks-api/).&#x20;

{% hint style="warning" %}
For now this feature is only available through API. if you want us to release it on merchant portal let us know [support](../support/how-to-contact-us.md) :e-mail:
{% endhint %}

## 2-Subscribe through merchant-webhooks API

**All the features described below and more are available though** [**`merchant-webhooks API`**](../api-reference/merchant-webhooks-api/).&#x20;

The logic is the same as described in above chapters.

### Configure your webhook endpoints url to listen events from one [event type](../api-reference/merchant-webhooks-api/#webhook-event-types) code with `API PUT /webhooks`

**At minimum one `"eventypecode"` is required** in the body of the request. The following values are possible:\
`"ANY"` if you want to listen all event types depending on your solutions subscription\
`{a dedicated "evenTypeCode"}` to listen all events from a dedicated event type code\
`"HELLO_WORD"` special value to test your configuration only\
\
other parameters are optional

{% hint style="info" %}
if you don't complete a configuration of a webhook url endpoint, events of the related "EventTypeCode" will be not sent **but all events will be stored waiting your retrieval with API GET /events.** This allow you to pull events instead of getting requested on the fly.
{% endhint %}

`"active":` true make your configuration active,\
`"url":` enter your webhook url endpoint

security fields `[authMethod;authLogin ...]`: see above chapter\
`"emailForAlerts":` enter an email address to receive alerts when an event is triggered on your webhook\
`"activeEventCodes":` list of "eventsCodes" you want to listen. by default all eventsCodes from the mentionned "eventTypeCode" are listenned&#x20;

{% code title="Example PUT  /webhooks" %}
```json
{
  "eventTypeCode": "SC_SUBSCRIPTION",
  "active": true,
  "url": "https://www.acme.com/webhooks/events/credit",
  "authMethod": "BASIC_AUTH",
  "authLogin": "mySuperLogin",
  "authPassword": "mySuperPassword",
  "authScope": "mySuperScope",
  "keyForSignature": "e5399af3ebcde0f3ead45086e13e932f36b1e5a1db002c8bb6a2870a1d22a7b6",
  "secret": "mySuperSecretOrMyAPIKey",
  "emailForAlerts": "support@acme.com",
  "activeEventCodes": [
    "SC_SUBSCRIPTION_ACCEPTED",
    "SC_SUBSCRIPTION_REJECTED"
  ]
}
```
{% endcode %}

You can Verify your configuration with `API GET /webhooks`Test your webhook endpoint with `API /events/tests/_trigger` to trigger an `"HELLO_WORLD"` event

This will trigger an event "HELLO\_WORLD" to the dedicated configuration. No parameter are required. Event received is factice and will be structured as normal event but with "HELLO\_WORD" payload data.

{% code title="Example "HELLO_WORLD" event" %}
```json
{
  "timestamp": "2023-11-02T01:30:00.00Z",
  "id": "bf6f6023-93a2-4266-9a2c-3579d803c09c",
  "correlationId": "7d9670fe-a0cf-4073-afde-bdc61ca49f75",
  "eventTypeCode": "HELLO_WORLD",
  "eventCode": "HELLO_WORLD",
  "data": {
    "eventTypeCode": "HELLO_WORLD",
    "eventCode": "HELLO_WORLD",
    "helloWorldMessage": "HELLO_WORLD"
    }
}
```
{% endcode %}

### Consume webhooks events

Once your configuration is tested and activated you will received automatically events on your webhook url. Each event would be structured as:

{% code title="Event request Body structure" overflow="wrap" %}
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
{% endcode %}

{% hint style="info" %}
"Data" structure is depending on related "eventTypeCode". see more details on [event types](../api-reference/merchant-webhooks-api/webhook-event-types.md).&#x20;
{% endhint %}

Once processed by your server and response is 200 OK, event is considered as consumed and will not be resent.

If the response <> 200 OK, then event is considered as not consumed and a replay operation will occurs according the replay mechanism (every 10 minutes during 10 days). Each replay operation will be counted.&#x20;

### Retrieve webhooks events

At any moment, you can retrieve events sent with [`API /events`](../api-reference/merchant-webhooks-api/)filtered by status `[OK| ERROR|INACTIVE |NO_CONFIG]` or a specific "eventTypeCode" or "eventCode" for a period.&#x20;

Status meaning:

* OK: Event with status 200 OK
* ERROR :  event with status <> 200 OK
* INACTIVE: event with configuration inactive
* NO\_CONFIG: event with incomplete (no url) configuraton.&#x20;

{% hint style="info" %}
Even if configuration is inactive or incomplete, you can retrieve events you would have received other way. This allow you to pull events instead and getting it on the fly.&#x20;
{% endhint %}

A list of events with their status will be returned:

{% code title="List of events sent" %}
```json
{
  "totalEventCount": 5,
  "events": [
    {
      "timestamp": "2023-11-02T01:30:00.00Z",
      "id": "bf6f6023-93a2-4266-9a2c-3579d803c09c",
      "correlationId": "7d9670fe-a0cf-4073-afde-bdc61ca49f75",
      "eventTypeCode": "SC_SUBSCRIPTION",
      "eventCode": "SC_SUBSCRIPTION_ACCEPTED",
      "data": {
        "eventTypeCode": "SC_SUBSCRIPTION",
        "eventCode": "SC_SUBSCRIPTION_ACCEPTED",
        "merchantGlobalOrderId": "340005489",
        "financedAmount": 119.9,
        "consolidatedStatus": "ACCEPTED"
      },
      "replayCount": 10,
      "status": "ERROR",
      "timestampOfLastDeliveryAttempt": "2023-01-29T10:05:38.429Z",
      "httpStatusCodeOfLastDeliveryAttempt": 401
    },
    {
      "timestamp": "2023-02-15T01:30:00.00Z",
      "id": "bf6f6023-93a2-4266-9a2c-3579d803c10c",
      "correlationId": "7d9670fe-a0cf-4073-afde-bdc61ca49f76",
      "eventTypeCode": "SC_SUBSCRIPTION",
      "eventCode": "SC_SUBSCRIPTION_REJECTED",
      "data": {
        "eventTypeCode": "SC_SUBSCRIPTION",
        "eventCode": "SC_SUBSCRIPTION_REJECTED",
        "merchantGlobalOrderId": "340005490",
        "financedAmount": 500.0,
        "consolidatedStatus": "REJECTED"
      },
      "replayCount": 0,
      "status": "ok",
      "timestampOfLastDeliveryAttempt": "2023-02-15T10:05:38.429Z",
      "httpStatusCodeOfLastDeliveryAttempt": 200
    },
    ...
  ]
}
```
{% endcode %}

### Verify signature of webhooks events (optional)

If you choose in your webhook configuration to enter a "keyForSignature" value then payload of events will be crypted using HMAC-SHA256 algorithm with a header X-BAAS-SIGNATURE.



&#x20; &#x20;
