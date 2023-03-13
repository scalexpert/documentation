---
description: 'How to initiate a e-financing journey: smart credit or split payment'
---

# Initiate a e-financing journey

## Initiate a financing journey with the [`Credit API`](../../api-reference/credit-api.md)&#x20;

Initiate a financing journey is 2 steps process:

1.  Display eligible e-financing solutions

    You can display all eligible [**e-financing solutions**](#user-content-fn-1)[^1] by calling API [`POST credit/0.0.1/credit/v1/eligible-solutions`](../../api-reference/credit-api.md#credit-v1-eligible-solutions) .&#x20;

    It can be used for displaying a insert text or graphical widget on the product page.

    Also, It can be used to display the  payment methods during the checkout process.

    There are mandatory input parameters such as "Amount to be financed" and "Country of Buyer" . As a result, you will get all eligible e-financing solutions to be used to initiate a subscription.
2.  Subscribe to a dedicated e-financing solutions

    After selecting a financing method you can initiate a subscription by calling [`API POST credit/v1/subscriptions`](../../api-reference/credit-api.md#credit-v1-subscriptions-1) &#x20;

    The request must be completed with all Buyer identities, billing & delivery addresses and basket content.&#x20;

    As a result, you will get a "subscription Id" and a "redirect Url" to redirect the buyer to start his e-financing journey that would vary accordingly to the financing method chosen.

{% hint style="info" %}
_Select a e-financing solution is mandatory before initiating a subscription._&#x20;
{% endhint %}

<figure><img src="../../.gitbook/assets/github - initiate e-financing solution.png" alt=""><figcaption><p>Flows: initiate a e-financing solution</p></figcaption></figure>

[^1]: e-financing are 2 kinds "Smart Credit" or "Split Payment". &#x20;
