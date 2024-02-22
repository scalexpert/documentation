---
description: How to follow your financing requests
---

# Prestashop financing requests follow-up

## 1- For Customers from the store

When a customer will request for a financing option (3X payment, credit ...) the order will be automatically created with a status "Awaiting financing".  The confirmation order page will display the latest status of their financing request.

At any moment, customers can follow their financing requests directly from the Prestashop store at the "account / order details and history" native Prestashop page.

{% hint style="info" %}
Customers will also interact directly with the financing institution during their financing   subscription and post-sales journeys. They will receive email and get access of the back-office of the  financing institution. This is independent of the order management in the Prestashop website. &#x20;
{% endhint %}

<figure><img src="../../../../.gitbook/assets/1-prestashop-financing-customer-followup (1).gif" alt=""><figcaption><p>How customers can follow their financing requests</p></figcaption></figure>

## 2-For Merchants from the back-office

Merchants can follow customers financing requests directly from the back-office at the "client order management" native Prestashop pages.

<figure><img src="../../../../.gitbook/assets/2-prestashop-financing-merchantfollowup.gif" alt=""><figcaption><p>How merchants can follow customers financing requests</p></figcaption></figure>

## 3- Financing request vs order management

When a financing request is "INITIALIZED" , then a new customer order is created in PRESTASHOP with a new status "Awaiting Financing".&#x20;

{% hint style="warning" %}
Please review in the PRESTASHOP back-office menu "configure/shop parameters/order settings/statuses" parameters for this new status "awaiting financing". For instance we recommend not to activate "sending a email" to the customer at that stage.
{% endhint %}

Then the financing customer journey start and PRESTASHOP will  collect status from financing institution automatically (See more details on financing requests statuses here [E-financing solutions life cycle](../../../../for-discovery/credit/e-financing-status-life-cycle.md)). Latest financing request status is displayed on order detail management (see new bloc "Financing subscriptions")  in PRESTASHOP back-office.

{% hint style="info" %}
Financing request statuses are collected at different times: after return of financing customer journeys, on periodic basis for asynchronous steps. Some mechanism for requesting statuses are in place (for more details see [advanced configuration guide](prestashop-advanced-features.md#2-set-up-pulling-financing-requests-updates)).
{% endhint %}

Mapping of financing requests and PRESTASHOP order statuses can be setup in the "scalexpert/admin" menu. So automatically, customer orders status will evolve accordingly.

<figure><img src="../../../../.gitbook/assets/Capture d’écran du 2024-02-22 19-03-27.png" alt=""><figcaption><p>mapping of financing and order statues</p></figcaption></figure>
