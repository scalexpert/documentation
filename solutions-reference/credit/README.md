---
description: Split payment and long term journeys
---

# e-Financing journeys

## Description

The **e-financing BaaS solution** allows you to easily trigger 2 kinds of journeys:

* Split Payment
* Long term credit

The 2 kinds are integrated with the  [`API e-Financing`](../../api-reference/e-financing-api/retired-versions-e-financing-api/v-1.0.md) . You will have to select the [`solution code` ](#user-content-fn-1)[^1]accordingly the combination depicted below and according what you have contracted.

#### E-financing solution codes

<table><thead><tr><th width="204">e-Financing solution</th><th width="98">Country</th><th width="138">Installments</th><th width="161">Conditions</th><th>Solution code</th></tr></thead><tbody><tr><td>Split payments</td><td>FR</td><td>3 times</td><td>Total subsidy (<a href="./#legend">1</a>)</td><td>SCFRSP-3XTS</td></tr><tr><td>Split payments</td><td>FR</td><td>3 times</td><td>Partial subsidy (<a href="./#legend">2</a>)</td><td>SCFRSP-3XPS</td></tr><tr><td>Split payments</td><td>FR</td><td>4 times</td><td>Total subsidy (<a href="./#legend">1</a>)</td><td>SCFRSP-4XTS</td></tr><tr><td>Split payments</td><td>FR</td><td>4 times</td><td>Partial subsidy (<a href="./#legend">2</a>)</td><td>SCFRSP-4XPS</td></tr><tr><td>Long term credit</td><td>FR</td><td>4-60 times</td><td>No fees for merchant, all fees to e-buyer</td><td>SCFRLT-TXNO</td></tr><tr><td>Long term credit</td><td>FR</td><td>4-60 times</td><td>Partial subsidy (<a href="./#legend">2</a>)</td><td>SCFRLT-TXPS</td></tr><tr><td>Long term credit</td><td>DE</td><td>6-48 times</td><td>Total subsidy (<a href="./#legend">1</a>)</td><td>SCDELT-DXTS</td></tr><tr><td>Long term credit</td><td>DE</td><td>6-48 times</td><td>Commission (<a href="./#legend">3</a>)</td><td>SCDELT-DXCO</td></tr></tbody></table>

#### Legend:

1. Total subsidy: merchant bear all fees, no fees for e-buyer&#x20;
2. Partial subsidy: merchant bear part of the fees, the rest for e-buyer
3. Commission: merchant is commissioned on the financing and e-buyer bear all fees &#x20;

## Step-by-Step

There is 2 steps to initiate & trigger an e-financing journey:&#x20;

1. Initiate an e-financing journey and select a solution code
2. Run the e-financing journey according the solution code selected

##

[^1]: A solution code will define what kind of journey you will trigger
