---
description: Split payment and long term journeys
---

# e-Financing journeys

## Description

The **e-financing BaaS solution** allows you to easily trigger 2 kinds of journeys:

* Split Payment
* Long term credit

The 2 kinds are integrated with the  [`API e-Financing`](../../api-reference/credit-api.md) . You will have to select the [`solution code` ](#user-content-fn-1)[^1]accordingly the combination depicted below and according what you have contracted.

#### E-financing solution codes

| e-Financing solution | Country | Installments | Fees          | Solution code |
| -------------------- | ------- | ------------ | ------------- | ------------- |
| Split payments       | FR      | 3 times      | No fees users | SCSPFR-3XTS   |
| Split payments       | FR      | 3 times      | Shared fees   | SCSPFR-3XPS   |
| Split payments       | FR      | 4 times      | No fees users | SCSPFR-4XTS   |
| Split payments       | FR      | 4 times      | Shared fees   | SCSPFR-4XPS   |
| Long term credit     | FR      | 4-60 times   |               | SCLTFR        |
| Long term credit     | DE      | 6-48 times   |               | SCLTDE        |

## Step-by-Step

There is 2 steps to initiate & trigger a e-financing journey:&#x20;

1. Initiate a e-financing journey and select a solution code
2. Run the e-financing journey according the solution code selected

##

[^1]: A solution code will define what kind of journey you will trigger
