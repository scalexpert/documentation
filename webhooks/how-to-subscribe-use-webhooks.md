---
description: Merchant webhooks tutorial (Work in progress)
---

# How to subscribe, use Webhooks

{% hint style="info" %}
Merchant Webhooks has just been released! :tada:  Pulling event via API method stay another good alternative (plugin integration is using pulling for now) but using webhooks especially for merchants with custom API integration that want instantness of information could be the solution.&#x20;
{% endhint %}

{% hint style="danger" %}
Nevertheless, webhooks method is more complex than pulling as it requires security skills such authorizing flows between our backends and your systems. Also, asynchronous flows could be more tricky to manage in case of network or system failure. so we recommend  to well study your need before starting. The reading of this guide would help you in your integration.&#x20;
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
When signature is used you would have to verify the signature before consuming event. See dedicated chapter "[Verify signature of webhook event"](how-to-subscribe-use-webhooks.md#verify-signature-of-webhooks-events-optional)  &#x20;
{% endhint %}

#### Configure your endpoint to listen events

Chose [events types](../api-reference/merchant-webhooks-api/webhook-event-types.md) to listen on the endpoint webhook url. Events types listed are the ones available for you that fit your solutions subscribed.

{% hint style="info" %}
You can listen multiple events types on the same endpoint. But we recommend subscribing separated endpoints because it will be easier to parse the payload according event type structure. see more details on event types [there](../api-reference/merchant-webhooks-api/webhook-event-types.md).&#x20;
{% endhint %}

### Manage webhooks endpoints

Once webhooks added, you can manage your webhooks endpoints at the webhooks tab. Manage webhooks allow you to change the configuration, activate/deactivate events.&#x20;

{% hint style="info" %}
You can activate/deactivate webhooks at any time for all events subscribed or events by events.&#x20;
{% endhint %}

{% hint style="danger" %}
Pay attention activation of weebhook is not immediate (only at first time) because we would need to declare your webhook url endpoint as authorized outbound flow (a delay of 6 open days would be necessary).

Also for security reasons, you may need to register IP address of our systems into your network configuration to authorized in-bounds flows. In case of, contact us to obtain range of IP adresses to configure.   &#x20;
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

**At minimum one `"evenTypeCode"` is required** in the body of the request. The following values are possible:\
`"ANY"` if you want to listen all event types depending on your solutions subscription\
`{a dedicated "evenTypeCode"}` to listen all events from a dedicated event type code\
`"HELLO_WORD"` special value to test your configuration only

**Complete your configuration with "url" and security attributes:**

`"url":` enter your webhook url endpoint (<mark style="color:red;">required if configuration active</mark>)

Security attributes (<mark style="color:red;">required if configuration active</mark>):

`"authMethod ":` choose among the authentication method available \[`None | Basic auth | API key]`\
Fields to complete according authentication method:

Mandatory fields <mark style="color:red;">\*</mark>

| None                                      | Basic auth                                      | API key                                             |
| ----------------------------------------- | ----------------------------------------------- | --------------------------------------------------- |
| secret <mark style="color:red;">\*</mark> | authLogin <mark style="color:red;">\*</mark>    | secret (API key) <mark style="color:red;">\*</mark> |
| keyForSignature                           | authPassword <mark style="color:red;">\*</mark> | keyForSignature                                     |
|                                           | keyForSignature                                 |                                                     |

{% hint style="warning" %}
Field "authScope" is depreciated. Please do not use it.&#x20;
{% endhint %}

Optional attributes:

`"emailForAlerts":` enter an email address to receive alerts when an event is not successfully delivered to your webhook

`"activeEventCodes":` list of "eventsCodes" you want to listen. by default all eventsCodes from the mentioned "eventTypeCode" are listened&#x20;

### Activate your configuration

You can update your configuration many times till attribute "`activate": false` is mentioned.&#x20;

`"active": true`  make your configuration active.

{% hint style="danger" %}
Pay attention activation of weebhook is not immediate (only at first time) because we would need to declare your webhook url endpoint as authorized outbound flow (a delay of 6 open days would be necessary).

Also for security reasons, you may need to register IP address of our systems into your network configuration to authorized in-bounds flows. In case of, contact us to obtain range of IP adresses to configure.&#x20;
{% endhint %}

{% hint style="danger" %}
Pay attention to activate your configuration ONLY if  you completed parameters "url" and "security fields" otherwise it will generate an error on production. We recommend strongly to [test your configuration](how-to-subscribe-use-webhooks.md#test-your-webhooks-configuration) with event "HELLO\_WORLD" before activating.
{% endhint %}

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
  "emailForAlerts": "mySupport@merchant.com",
  "activeEventCodes": [
    "SC_SUBSCRIPTION_ACCEPTED",
    "SC_SUBSCRIPTION_REJECTED"
  ]
}
```
{% endcode %}

### Test your configuration

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

Once processed by your server and response is 200 OK or 201 CREATED, event is considered as consumed and will not be resent.

{% hint style="warning" %}
The response body of your webhook MUST be empty.&#x20;
{% endhint %}

If the response <> 200 OK and 201 CREATED, then event is considered as not consumed and a replay operation will occur according the replay mechanism (every 10 minutes during 5 days). Each replay operation will be counted.&#x20;

### Retrieve webhooks events

At any moment, you can retrieve events sent with [`API /events`](../api-reference/merchant-webhooks-api/)filtered by status `[OK| ERROR|INACTIVE |NO_CONFIG]` or a specific "eventTypeCode" or "eventCode" for a period.&#x20;

Status meaning:

* OK: Event with status 200 OK or 201 CREATED
* ERROR :  event with status <> 200 OK and 201 CREATED
* INACTIVE: event with configuration inactive
* NO\_CONFIG: no configuration found for this event
* (KILLED): event killed by scalexpert support team for internal reason

{% hint style="info" %}
Even if a configuration is inactive or isn't found, you can still retrieve events through API GET /events. This functionality enables you to pull events on demand, allowing for more flexible data management.
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

In the webhook configuration, If you enter a "keyForSignature" value then for each event sent thse headers "X-BAAS-SIGNATURE" and "X-BAAS-SIGNATURE-TIMESTAMP" will be provided. "X-BAAS-SIGNATURE" header value will be computed using HMAC-SHA256 algorithm and combining the payload string of event and the "keyForSignature" value. This will ensure that payload of event are correct and not falsified by malevolent actor.

Thus, you would need to verify the header "X-BAAS-SIGNATURE" before parsing the event payload.

Header "X-BAAS-SIGNATURE-TIMESTAMP" is intended to check if event received is "freshly" sent and not a older one.

{% tabs %}
{% tab title="Verify signature 1/2" %}
{% code title="Java - sample of  function to verify the X-BAAS-SIGNATURE (1/2)" overflow="wrap" lineNumbers="true" %}
```java
**
* Example of a REST/JSON webhook endpoint with validation of the signature contained in the HTTP header X-BAAS-SIGNATURE.
*
* @param webhookEventAsString: Body of the http request as String. The body must be a JSON object with a structure compatible with the event format described in the developer portal.
* @param httpRequest:     The HttpServletRequest automatically injected by Spring (used to get headers)
* @return the response must be empty, the only important point is that you must return the status code 200-OK or 201-CREATED to acknowledge that the event has been taken into account/processed
* (if the returned status code is NOT 200-OK or 201-CREATED, the event will be retriggered/redelivered in few minutes)
*/
@PostMapping(value = "/webhooks/smart-credit-subscription", consumes = MediaType.APPLICATION_JSON_VALUE, produces = MediaType.APPLICATION_JSON_VALUE)
public ResponseEntity<Void> snippet_webhookForSmartCreditSubscription(@RequestBody String webhookEventAsString, HttpServletRequest httpRequest) {

    // Get the key to use to check the signature of the body of the http request. The key is defined by the merchant during the declaration of the webhook endpoint in the merchant portal.
    String keyForSignature = "123456";

    // Check if the signature of the request body (with keyForSignature) and the signature in the HTTP header X-BAAS-SIGNATURE match
    boolean isSignatureValid = snippet_isSignatureValid(webhookEventAsString, keyForSignature, httpRequest);

    if (isSignatureValid) {
        // If the signature is valid...
        //      parse the webhookEventAsString to some POJO class WebhookEvent ...
        //      process the webhookEvent...
        //      return the status code 200-OK or 201-CREATED
        return ResponseEntity.ok().build(); // The response body must be empty, only the returned HTTP status code is important
    } else {
        // If the signature is NOT valid...
        //      return the status code 400-BAD-REQUEST (could be also 403-FORBIDDEN...)
        return ResponseEntity.badRequest().build(); // The response body must be empty, only the returned HTTP status code is important
    }
}
```
{% endcode %}
{% endtab %}

{% tab title="Verify signature 2/2" %}
{% code title="Java - sample of  function to verify the X-BAAS-SIGNATURE (2/2)" overflow="wrap" lineNumbers="true" %}
```java
/**
 * This operation is used to check that the received event (on a HTTP REST/JSON webhook endpoint) has been triggered
 * by a trusted source (like BaaS/ScaleExpert) and has not been altered/modified by an intermediary component (man-in-the-middle attack).
 * @param webhookEventForMerchantAsString: Body of the http request as String. The body must be a JSON object with a structure compatible with the event format described in the developer portal.
 * @param keyForSignature: Key to use to check the signature of the body of the http request. The key is defined by the merchant during the declaration of the webhook endpoint in the merchant portal.
 * @param httpRequest:     The HttpServletRequest automatically injected by Spring (used to get headers)
 * @return true if the signature of the body (with keyForSignature) and the signature in the HTTP header X-BAAS-SIGNATURE match.
 */
public boolean snippet_isSignatureValid(String webhookEventForMerchantAsString, String keyForSignature, HttpServletRequest httpRequest) {
    String HTTP_HEADER_FOR_BAAS_SIGNATURE = "X-BAAS-SIGNATURE";
    String HTTP_HEADER_FOR_BAAS_SIGNATURE_TIMESTAMP = "X-BAAS-SIGNATURE-TIMESTAMP";

    // If there is no Signature header, then there is no signature to check, so we consider it is ok to continue
    String valueOfSignatureHttpHeader = httpRequest.getHeader(HTTP_HEADER_FOR_BAAS_SIGNATURE);
    if (valueOfSignatureHttpHeader == null || valueOfSignatureHttpHeader.isEmpty()) {
        return true;
    }

    String timestampInHttpHeaderAsString = httpRequest.getHeader(HTTP_HEADER_FOR_BAAS_SIGNATURE_TIMESTAMP);
    if (timestampInHttpHeaderAsString == null || timestampInHttpHeaderAsString.isEmpty()) {
        throw new RuntimeException("Timestamp is missing in HTTP Header " + HTTP_HEADER_FOR_BAAS_SIGNATURE_TIMESTAMP);
    }
    String hmacInHtpHeaderAsString = httpRequest.getHeader(HTTP_HEADER_FOR_BAAS_SIGNATURE);    // never null nor empty because of the test at the very beginning of this operation

    // Check that the timestamp is close to now (less than 5 minutes)

    boolean isTimestampCloseToNow;
    DateTimeFormatter fmt = DateTimeFormatter.ISO_INSTANT.withZone(ZoneOffset.UTC);
    Instant timestampInHttpHeader = null;
    try {
        timestampInHttpHeader = Instant.from(fmt.parse(timestampInHttpHeaderAsString));
    } catch (Exception ex) {
        String errMsg = "Error while parsing timestamp " + timestampInHttpHeaderAsString;
        telemetry.error(errMsg, ex);
        throw new RuntimeException(errMsg, ex);
    }
    isTimestampCloseToNow = Instant.now().minusSeconds(MAX_AGE_IN_SECONDS_FOR_SIGNATURE_TIMESTAMP).isBefore(timestampInHttpHeader);

    // Check that the hmac is ok

    String payloadToSign = timestampInHttpHeaderAsString + "." + webhookEventForMerchantAsString;
    String hmacOfTheBody = snippet_hmacSHA256(payloadToSign, keyForSignature);
    boolean areHmacEqual = hmacOfTheBody.equalsIgnoreCase(hmacInHtpHeaderAsString);

    // The signature is ok if the hmac SHA 256 is ok and the timestamp is ok
    return areHmacEqual && isTimestampCloseToNow;
}
```
{% endcode %}
{% endtab %}

{% tab title="Utility hmac" %}
{% code title="Java - Utility operation to generate a hmac of some String using SHA256." overflow="wrap" lineNumbers="true" %}
```java
/**
 * Utility operation to generate a hmac of some String using SHA256.
 * @param clearText: String in clear text for which we want to calculate the hmac.
 * @param key: Key to use to calculate the hmac.
 * @return the hmac of the string using SHA256.
 */
private String snippet_hmacSHA256(String clearText, String key) {
    try {
        SecretKeySpec secretKeySpec = new SecretKeySpec(key.getBytes(), "HmacSHA256");
        Mac mac = Mac.getInstance("HmacSHA256");
        mac.init(secretKeySpec);
        byte[] encryptedText = mac.doFinal(clearText.getBytes());
        return Hex.encodeHexString(encryptedText);

    } catch (Exception ex) {
        String errMsg = String.format("Error while calculating hmacSHA256. Error was %s", ex.getMessage());
        throw new RuntimeException(errMsg, ex);
    }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}
