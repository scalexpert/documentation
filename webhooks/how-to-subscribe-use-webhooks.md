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



