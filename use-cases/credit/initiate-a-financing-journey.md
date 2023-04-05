---
description: 'How to initiate a e-financing journey: smart credit or split payment'
---

# Initiate a e-financing journey

## Initiate a e-financing journey with the [`Credit API`](../../api-reference/e-financing-api.md)&#x20;

Initiate a financing journey is 2 steps process:

1.  Display eligible e-financing solutions

    You can display all eligible [**`e-financing solutions codes`**](./#e-financing-solution-codes) by calling API [`POST credit/0.0.1/credit/v1/eligible-solutions`](../../api-reference/e-financing-api.md#credit-v1-eligible-solutions) .&#x20;

    There are mandatory input parameters such as "Amount to be financed" and "Country of the Buyer" . \
    As a result, you will get all eligible e-financing solutions codes to be selected to initiate a subscription.\
    It will also return the "merchant kit" you can used to display a insert text or graphical widget on the product page explaining the solution to the buyer with the general conditions.\
    <mark style="background-color:yellow;">mettre ici un exemple d'insert graphique pour le crédit</mark>

    Also, It can be used to display the  payment methods during the checkout process.
2.  Subscribe to a dedicated e-financing solutions

    After selecting a financing method you can initiate a subscription by calling [`API POST credit/v1/subscriptions`](../../api-reference/e-financing-api.md#credit-v1-subscriptions-1) &#x20;

    The request must be completed with buyer identities, billing, delivery addresses and basket content.&#x20;

    As a result, you will get a "subscription Id" and a "redirect Url" to redirect the buyer to start his e-financing journey that would vary accordingly to the financing solution code selected.

{% hint style="info" %}
_Initiating a subscription with a specific e-financing solution code is a prerequisite before executing any e-financing buyer journey._ &#x20;
{% endhint %}

<figure><img src="../../.gitbook/assets/github - initiate e-financing solution.png" alt=""><figcaption><p>Flows: initiate a e-financing solution</p></figcaption></figure>
