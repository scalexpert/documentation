---
description: Collect your API keys and secrets from your developer space (merchant portal)
---

# 🆕 API key

{% hint style="success" %}
This is a new feature replacing former access to the [developer portal](../../api-reference/apis-common/api-console-advance-features/) (API console). API console would be still available for advanced needs.
{% endhint %}

{% hint style="danger" %}
For security reasons API key secret would be never sent by email. The only way to display it would be at reset operation! For more details please consult our [security best practices.](../../security/security-best-practices.md)&#x20;
{% endhint %}

Get your API keys in 3 steps:

{% tabs %}
{% tab title="1-Access the developer menu" %}
Once connected to the merchant portal, access your "developer space" by clicking on the menu  "DEVELOPER "and sub-menu "API Keys".

<figure><img src="../../.gitbook/assets/cléapi1a.png" alt=""><figcaption><p>access the developer menu "API Key" page</p></figcaption></figure>
{% endtab %}

{% tab title="2-API key page" %}
API key page will display your 2 kind of Keys:\
\- 1 API key test (UATC)\
\- 1 API key production (PROD)\
for more details on environment please consult our [API reference guide](../../api-reference/apis-common/api-urls.md).&#x20;

For each API key, you will see an Identifier (client Id) that have been generated.&#x20;

Important: an empty key (client Id) would mean that your "on boarding key activation" step is not yet completed or something wrong. If so please [contact support team](../../support/how-to-contact-us.md#contact-support) :e-mail:

<figure><img src="../../.gitbook/assets/cléapi1b (1).png" alt=""><figcaption><p>API keys test and production</p></figcaption></figure>
{% endtab %}

{% tab title="3-Reset secret" %}
Choose your API key test or production and click on "reset" button to obtain your secret

<figure><img src="../../.gitbook/assets/cléapi1c.png" alt=""><figcaption><p>reset your secret key</p></figcaption></figure>

A confirmation page will be displayed **because this operation is irrevocable** !

<figure><img src="../../.gitbook/assets/cléapi2.png" alt=""><figcaption><p>confirm reset operation</p></figcaption></figure>

A new secret will be created and displayed. **Copy it and store it securely** (see [security best practices](../../security/security-best-practices.md)) because **it will be not possible to display after.** But at anytime, you can redo resetting operation as much as you would need.

<figure><img src="../../.gitbook/assets/cléapi3a.png" alt=""><figcaption><p>your secret have been generated successfully</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/cléapi4a (1).png" alt=""><figcaption><p>Display or copy your secret</p></figcaption></figure>
{% endtab %}

{% tab title="Verify your secret" %}
At any time you can verify your secret!

<figure><img src="../../.gitbook/assets/cléapi1d.png" alt=""><figcaption><p>verify your secret</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/cléapi5a.png" alt=""><figcaption><p>enter your secret to verify</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/cléapi6.png" alt=""><figcaption><p>your secret has been verified successfully!</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/cléapi7.png" alt=""><figcaption><p>your secret is not corresponding to your key!</p></figcaption></figure>
{% endtab %}
{% endtabs %}

