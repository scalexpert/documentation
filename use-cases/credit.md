---
description: un texte court marketing décrivant l'offre smart crédit
---

# SmartCredit

## Description

The credit features of the BaaS solution allows you to easily integrate credit offers into your e-commerce shop. Our credit API allows you to easily access a wide range of long and short term credit offers in different geographical markets.

## Features

_Tableau crédit court/long + FR/DE + coming soon_

prévoir une description step by step du parcours avec des illustrations si-possible cf. exemple [https://docs.almapay.com/docs/products-pay-in-installments](https://docs.almapay.com/docs/products-pay-in-installments)

## Flows

ajouter un diagramme de séquence simplifié des flux d'APIs pour expliquer comment fonctionne le produit et quelles APIs le marchand doit utiliser (cf. exemple [https://doc.fintecture.com/reference/immediate-payment](https://doc.fintecture.com/reference/immediate-payment)&#x20;

## Initiate a financing journey with the [`Credit API`](../api-reference/credit-subscriptions.md)&#x20;

Initiate a financing journey is 2 steps process:

1.  Display eligible financing methods

    You can display all eligible [**financing methods**](#user-content-fn-1)[^1] by calling API `POST` `credit/v1/financingMethods/_eligible` .&#x20;

    It can be use for displaying a insert text or graphical widget on the product page, and to display the  payment methods during the checkout process.

    There are mandatory input parameters such as "Amount to be financed" and "Country of Buyer" . As a result, you will get all eligible `financingMethodCode` eligible with a details such as descriptions text, conditions text, visual logo ...&#x20;

    _**Select a financing methods is mandatory before initiating a subscription.**_&#x20;
2.  Subscribe to a dedicated financing method

    After selecting a financing method you can initiate a subscription by calling API [`POST credit/v1/subscriptions` ](../api-reference/credit-subscriptions.md#v1-subscriptions)&#x20;





<figure><img src="../.gitbook/assets/smartcredit flows - initiate financing journey (1).png" alt=""><figcaption><p>Flows: initiate a financing credit journey</p></figcaption></figure>

[^1]: A "financing method" define the financing mean a buyer can choose among 3X times 4X times differed payments or LT Long credit
