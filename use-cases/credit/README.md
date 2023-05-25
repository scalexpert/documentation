---
description: Split payment and long term journeys
---

# e-Financing journeys

## Description

The **e-financing BaaS solution** allows you to easily trigger 2 kinds of journeys:

* Split Payment
* Long term credit

The 2 kinds are integrated with the  [`API e-Financing`](../../api-reference/e-financing-api/v-1.0.md) . You will have to select the [`solution code` ](#user-content-fn-1)[^1]accordingly the combination depicted below and according what you have contracted.

#### E-financing solution codes

<table><thead><tr><th width="204">e-Financing solution</th><th width="98">Country</th><th width="138">Installments</th><th width="143">Fees</th><th>Solution code</th></tr></thead><tbody><tr><td>Split payments</td><td>FR</td><td>3 times</td><td>No fees users</td><td>SCFRSP-3XTS</td></tr><tr><td>Split payments</td><td>FR</td><td>3 times</td><td>Shared fees</td><td>SCFRSP-3XPS</td></tr><tr><td>Split payments</td><td>FR</td><td>4 times</td><td>No fees users</td><td>SCFRSP-4XTS</td></tr><tr><td>Split payments</td><td>FR</td><td>4 times</td><td>Shared fees</td><td>SCFRSP-4XPS</td></tr><tr><td>Long term credit</td><td>FR</td><td>4-60 times</td><td></td><td>SCFRLT</td></tr><tr><td>Long term credit</td><td>DE</td><td>6-48 times</td><td></td><td>SCDELT</td></tr></tbody></table>

## Step-by-Step

There is 2 steps to initiate & trigger an e-financing journey:&#x20;

1. Initiate an e-financing journey and select a solution code
2. Run the e-financing journey according the solution code selected

##

[^1]: A solution code will define what kind of journey you will trigger
