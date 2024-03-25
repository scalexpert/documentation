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

| None                                      | Basic auth                                          | API key                                   |
| ----------------------------------------- | --------------------------------------------------- | ----------------------------------------- |
| Signature key                             | Identifier/login <mark style="color:red;">\*</mark> | Signature key                             |
| Secret <mark style="color:red;">\*</mark> | Password <mark style="color:red;">\*</mark>         | Secret <mark style="color:red;">\*</mark> |
|                                           | Signature key                                       |                                           |
|                                           | Secret                                              |                                           |

Identifier/login and password fields are required for basic auth only.

Secret is required for authentication None or API key. Secret is a string shared between you and scalexpert.&#x20;

Signature key is optional field for encrypting the body of the request. This add more security if needed.

{% hint style="warning" %}
When signature is used you would need to decrypt the body of the request by using a dedicated algorithm. see dedicated chapter "Decrypt webhook payload event"  &#x20;
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
other parameters are optional\
`"active":` true make your configuration active,\
`"url":` enter your webhook url endpoint\
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

You can Verify your configuration with `API GET /webhooks`

### Test your webhook endpoint with `API /events/tests/_trigger` to trigger an `"HELLO_WORLD"` event

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
    "eventCode": "HELLO_WORLD"
  },
  "replayCount": 0,
  "status": "OK",
  "timestampOfLastDeliveryAttempt": "2023-01-29T10:05:38.429Z",
  "httpStatusCodeOfLastDeliveryAttempt": 200
}
```
{% endcode %}
