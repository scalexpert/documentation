---
description: 'How to initiate an e-financing journey: split payment or long term credit'
---

# Initiate an e-financing journey

## Initiate an e-financing journey with the [`e-Financing API`](../../api-reference/e-financing-api/)&#x20;

Initiate an e-financing journey is 2 steps process:

1.  Display  eligible e-financing solutions

    You can display all eligible [**`e-financing solutions codes`**](./#e-financing-solution-codes) by calling API [`GET /e-financing/api/v1/eligible-solutions`](../../api-reference/e-financing-api/) .&#x20;

    There are mandatory input parameters such as "Amount to be financed" and "Country of the Buyer" . \
    As a result, you will get all eligible e-financing solutions codes to be selected to initiate a subscription.\
    It will also return the "merchant kit" you can used to display a insert text or graphical widget on the product page explaining the solution to the buyer with the general conditions.\
    Also, It can be used to display the  payment methods during the checkout process.
2. Simulate e-financing solutions\
   You can simulate any eligible [**`e-financing solutions codes`**](./#e-financing-solution-codes) by calling API [`POST /e-financing/api/v1/simulate-solutions`](../../api-reference/e-financing-api/). \
   As a result, you will have a list of simulations you can display on the product page so e-buyer can see details of the payments or credits installments and amounts. \
   You can see an example of the rendering of that simulations [here](../showcasing-solutions.md).
3.  Subscribe to a dedicated e-financing solutions

    After selecting a financing method you can initiate a subscription by calling [`API POST e-financing/api/v1/subscriptions`](../../api-reference/e-financing-api/) &#x20;

    The request must be completed with buyer identities, billing, delivery addresses and basket content.&#x20;

    As a result, you will get a "subscription Id" and a "redirect Url" to redirect the buyer to start his e-financing journey that would vary accordingly to the financing solution code selected.

{% hint style="info" %}
Want to know our showcasing our solutions on your website? Please refers to this [guide](../showcasing-solutions.md).
{% endhint %}

{% hint style="warning" %}
_Initiating a subscription with a specific e-financing solution code is a prerequisite before executing any e-financing buyer journey._ &#x20;
{% endhint %}

<figure><img src="../../.gitbook/assets/Simulate and initiate e-financing solution.png" alt=""><figcaption><p>Simulate and initiate an e-financing solution</p></figcaption></figure>
