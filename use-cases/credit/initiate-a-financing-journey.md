# Initiate a financing journey

## Initiate a financing journey with the [`Credit API`](../../api-reference/credit-subscriptions.md)&#x20;

Initiate a financing journey is 2 steps process:

1.  Display eligible financing methods

    You can display all eligible [**financing methods**](#user-content-fn-1)[^1] by calling API `POST` `credit/v1/financingMethods/_eligible` .&#x20;

    It can be used for displaying a insert text or graphical widget on the product page.

    Also, It can be used to display the  payment methods during the checkout process.

    There are mandatory input parameters such as "Amount to be financed" and "Country of Buyer" . As a result, you will get all eligible `financingMethodCode` to be used to initiate a suscription.
2.  Subscribe to a dedicated financing method

    After selecting a financing method you can initiate a subscription by calling API [`POST credit/v1/subscriptions` ](../../api-reference/credit-subscriptions.md#v1-subscriptions)&#x20;

    The request must be completed with all Buyer identities, billing & delivery addresses and basket content.&#x20;

    As a result, you will get a "subscription Id" and a "redirect Url" to redirect the buyer to start his financing journey that would vary accordingly to the financing method chosen.

{% hint style="info" %}
_Select a financing methods is mandatory before initiating a subscription._&#x20;
{% endhint %}

<figure><img src="../../.gitbook/assets/github - smartcredit flow (1).png" alt=""><figcaption><p>Flows: initiate a financing credit journey</p></figcaption></figure>

[^1]: A "financing method" define the financing mean a buyer can choose among 3X times 4X times differed payments or LT Long credit
