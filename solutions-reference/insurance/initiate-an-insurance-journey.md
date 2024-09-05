# Initiate an insurance journey

## Initiate an insurance journey with the [`insurance API`](../../api-reference/insurance-api/)&#x20;

The initiation of an insurance journey is a 3 step process:

1.  **Display eligible insurances solutions**

    You can display all eligible [**`Insurance solutions codes`**](./#insurance-solutions-codes) by calling [API `POST /insurance/api/v1/eligible-solutions`](../../api-reference/insurance-api/) .&#x20;

    The mandatory input parameter is the  "Country of the Buyer" . \
    As a result, you will get all eligible insurance solutions codes to be selected to initiate a insurance journey.\
    It will also return the "merchant kit" which you can use to display a insert text or graphical widget on the product page explaining the solution to the buyer with the general conditions.\
    It can be used to display the insurance solutions during the checkout process or within an intermediary page before checkout.
2. **Register items catalog** \
   Choose solution an [insurance solution code](./#insurance-solutions-codes)\
   Register each catalog items you want to search for insurances by calling [`API POST /insurance/api/v1/items`](../../api-reference/insurance-api/). You can register each Items on the fly or register the entire calalog once. The second option will allow you to anticipate testing eligibility of your items.\
   **Tips:** if you register twice the same item with same characteristics it will return the same item id.
3. **Search Items insurance's**\
   Choose solution an [insurance solution code](./#insurance-solutions-codes)\
   For each insurance solution, search eligible insurances for an item of your catalog by calling [`API POST /insurance/api/v1/items/_search-insurances`](../../api-reference/insurance-api/) _._\
   Register your catalog item and search for eligible insurance and warranties.&#x20;

{% hint style="info" %}
Want to know how to showcase our solutions on your website? Please refers to this [guide](../showcasing-solutions.md).
{% endhint %}

{% hint style="warning" %}
_Initiating a subscription with a specific insurance solution code and warranties are a prerequisite before subscribing._ &#x20;
{% endhint %}

<figure><img src="../../.gitbook/assets/Initiate Insurance journey (France).png" alt=""><figcaption><p>Display Eligible Insurance Item solutions</p></figcaption></figure>
