---
description: Useful data for testing purposes
---

# Testing solutions

{% hint style="info" %}
Prerequisites: You will need to get a customer account and a test key before testing our solutions. For more details see "[Before you start"](../ready-to-start/before-you-start/) guide. (no sandbox available yet !)&#x20;
{% endhint %}

### e-Financing solutions

French split payment journey will require to fill in a French card bank number

French Long credit journey will require to fill in an IBAN and also download identity documents to complete KYC steps. To follow the "happy path" use real identity documents to complete the KYC step and put a finance amount lower than 3000 € to be automatically accepted.

German long credit journey will require to fill in an German IBAN and KYC pin codes

<details>

<summary>French card bank numbers for testing purposes</summary>

* ACCEPTED (CB) - 5017 6791 1038 0400
* REFUSED (CB) - 5017 6791 1038 0900
* ACCEPTED (VISA) - 5017 6792 1000 0700
* REFUSED (VISA) - 5017 6792 1000 0200
* ACCEPTED (Mastercard) - 5017 6794 1000 0500
* REFUSED (Mastercard) - 5017 6794 1000 0000

</details>

<details>

<summary>French IBAN  codes for testing purposes</summary>

Test IBAN [https://fr.iban.com/testibans](https://fr.iban.com/testibans)&#x20;

</details>

<details>

<summary>German IBAN code for testing purposes</summary>

DE95100000000012305678

</details>

<details>

<summary>German KYC pin codes for testing purposes</summary>

**KYC pin codes**:\
\- for successful KYC use 123456\
\- for unsuccessful KYC use 654321&#x20;

**Important:** you have to type in a real mobile number to receive the final SMS for signature

</details>

### Insurance solutions

Please use these products for insurances tests

{% file src="../.gitbook/assets/Insurance_items_list (1).xlsx" %}
Insurance Items list
{% endfile %}

### Support

For any other test cases contact our integration support team [sg-ecommerce-support.world@socgen.com](mailto://sg-ecommerce-support.world@socgen.com)&#x20;
