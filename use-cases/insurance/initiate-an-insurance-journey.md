# Initiate an insurance journey

## Initiate an insurance journey with the [`insurance API`](../../api-reference/insurance-api/)&#x20;

Initiate an insurance journey is 2 step process:

1.  Display eligible insurances solutions

    You can display all eligible **`Insurance solutions codes`** by calling API [`POST /insurance/api/v1/eligible-solutions`](../../api-reference/insurance-api/v-1.0.md#insurance-v1-eligible-solutions) .&#x20;

    There are mandatory input parameter as "Country of the Buyer" . \
    As a result, you will get all eligible insurance solutions codes to be selected to initiate a insurance journey.\
    It will also return the "merchant kit" you can used to display a insert text or graphical widget on the product page explaining the solution to the buyer with the general conditions.\
    Also, It can be used to display the insurance solutions during the checkout process.
2. For each insurance solution search eligible insurances for an item of your catalog\
   Register your catalog item and search for eligible insurance  and garanties.&#x20;

{% hint style="info" %}
Want to know our showcasing our solutions on your website? Please refers to this [guide](../showcasing-solutions.md).
{% endhint %}

{% hint style="warning" %}
_Initiating a subscription with a specific insurance solution code and garanties are a prerequisite before subscribing._ &#x20;
{% endhint %}

<figure><img src="../../.gitbook/assets/Initiate insurance journey France (1).png" alt=""><figcaption><p>Display Eligible Insurance Item solutions</p></figcaption></figure>
