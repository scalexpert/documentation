---
description: How to integrate e-financing solutions via your PSP
---

# 🚧 PSP integration (e-financing only)

{% hint style="info" %}
New feature coming soon. [Contact us](../../support/how-to-contact-us.md) if interested
{% endhint %}

## Description

{% hint style="warning" %}
This mode is only available to integrate e-financing solutions.
{% endhint %}

A new possibility for e-financing solutions integration is available when as a merchant you are already integrated through a payment gateway of a PSP[^1].&#x20;

If it is your case, you can easily integrate e-financing solutions as another payment means in the list provided by the PSP.&#x20;

{% hint style="info" %}
The list of PSP available is under construction and will be communicated soon.
{% endhint %}

## Step-by-step integration

### 1. On boarding

During your merchant on boarding, inform your sales support team you want a "PSP integration mode" for e-financing solutions and provide your  "[**Client PSP reference code**](#user-content-fn-2)[^2]**"**  to be registered by RMS back-ends.&#x20;

{% hint style="info" %}
If you don't know your "Client PSP reference code" please contact your PSP.
{% endhint %}

### 2. Activation of e-financing solutions

Once the "RMS contract" is signed, activation tasks will be operated directly with your PSP. **You will have nothing to do** **with us** but your PSP will contact you to test integration results.  &#x20;

{% hint style="warning" %}
Please pay attention that this choice of integration of e-financing solutions has some consequences on the way of using related events webhooks.  Because it will be your PSP that will integrate and receive events instead of you as a merchant.&#x20;
{% endhint %}

And that's all !!! :tada:

## Technical requirements for PSPs

### API  Integration

As a PSP, you will have to use the same [API endpoints](../../api-reference/e-financing-api/) as a merchant but **you will receive a dedicated API key** that will allow you to call API endpoints **on behalf of merchants.**&#x20;

{% hint style="info" %}
As a PSP you will receive one API key for all your merchants. This will avoid integrating API keys each time you onboard a new merchant and during API calls.
{% endhint %}

[Documentation of API ](../../api-reference/e-financing-api/)is the same except you will have to provide one additional information as a header of the requests:

Header to be provide: `X-BAAS-CLIENT-REF-FOR-PROXI-ID`

{% code title="Sample of API request" overflow="wrap" %}
```bash
curl --location 'https://api.scalexpert.uatc.societegenerale.com/baas/uatc/e-financing/api/v1/eligible-solutions?financedAmount=500&buyerBillingCountry=FR' \
--header 'X-BAAS-CLIENT-REF-FOR-PROXI-ID: {REPLACE BY PSP MERCHANT REFEFRENCE CODE}' \
--header 'Authorization: Bearer eyJlbmMiOiJBMjU2Q0JDLUhT...uOd2XOFU5XizYWQQOKYWZ7XFRlTVPiDO0n6n7js.ok0LOHchQ-geaqy_DenjtgxNnp2jzZEGJMzXBcNdu40'
```
{% endcode %}

As explained before, as a PSP you will have to provide the Merchant's reference code for each API call. Thus RMS back-end will recognize it as registered during the "on boarding" by the merchant.

### Webhook integration

If you want to receive events through webhook endpoints, you will have to integrate only once independently of merchants integrations. You will receive all your PSP merchants events with additional header `X-BAAS-CLIENT-REF-FOR-PROXI-ID` allowing you to dispatch them by merchant.

[^1]: PSP is Payment Service Provider

[^2]: Your reference code as a client known by your PSP.&#x20;
