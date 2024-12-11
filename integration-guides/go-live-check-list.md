---
description: Check-list for go-live
---

# Go-Live check-list

## Go-Live check list

* [x] Check environments urls\
  Make sure you are using the right urls accordingly your environment purpose. Please consult  our API documentation [here](../api-reference/apis-common/api-urls.md).
* [x] Integrate the "[communication kit](../solutions-reference/showcasing-solutions.md)" in your website \
  Incorporate marketing and legal texts, such as "General Terms and Conditions" and "Brand Guidelines," into your materials. Ensure relevance for insurance or e-financing products. Those resources are provided trough [`API GET /eligible-solutions`](../api-reference/e-financing-api/)
* [x] Integrate  "general terms & conditions" of e-financing products into your website\
  Please add to your site a page with "general terms and conditions" of e-financing products. \
  For FRANFINANCE, please download the text in below [section.](go-live-check-list.md#franfinance-legal-terms-and-conditions-text-to-be-added-to-your-site) \

* [x] Make API integration tests\
  In any case we strongly recommend to test our solutions before go-live. In that purpose we gave you a test API key ([UATC environment](../api-reference/apis-common/api-urls.md#test-for-customer-uatc)) in order to use it on your own test environment.\
  \
  **E-financing solutions only:**\
  To test our solutions before going live, you must execute payments or create financing. \
  \
  Tests to be executed:
  * [ ] Split payment (3X, 4X) : acceptance and rejection tests for each solution in test environment, plus 1 acceptance test in production that will be cancelled by you 24 hours after FRANFINANCE verification.&#x20;
  * [ ] Long credit: pre-accepted, rejected and cancellation tests  in test environment.\
    \
    Please send us the document, **"PV de recette,"** to attest to the success of the tests. Download the "PV de recette" from FRANFINANCE e-financing solutions below.\

* [x] Change and store securely your APIs keys and secrets\
  Please pay attention to store securely your API keys and secrets on server side only. Consult our security documentation [here](broken-reference).&#x20;

## Warnings

{% hint style="danger" %}
Pay attention that you are not using your test and production keys **on the same environment**. If you do so, then **you must delete all test data** before switching into production otherwise you may encounter errors (especially e-financing subscriptions data) . We strongly recommend to use different environments for Test and Production purposes.
{% endhint %}

{% hint style="danger" %}
Ensure you receive our test validation acknowledgment before running e-financing solutions in production.
{% endhint %}

## Downloads

{% file src="../.gitbook/assets/PV RECETTE 3X4X - ScaleXpert.docx" %}
PV de recette FRANFINANCE 3X 4X solutions (split payment)
{% endfile %}

{% file src="../.gitbook/assets/PV RECETTE CREDIT LONG - ScaleXpert.docx" %}
PV de recette FRANFINANCE long credit solution
{% endfile %}

<details>

<summary>FRANFINANCE legal terms and conditions text to be added to your site</summary>

Commande réglée en 3X / 4X par carte bancaire, via Scalexpert :

&#x20;                                 Le paiement en 3 ou 4 fois par carte bancaire est une solution de paiement qui vous permet d’échelonner le règlement de votre commande en 3 ou 4 échéances débitées sur le compte associé à votre carte bancaire selon la formule retenue.

&#x20;

Lors de la mise en place de la solution de financement, les données liées à la commande du Client et ses données à caractère personnel, dont par exemple, ses données d’identification, sont transmises par le Vendeur à Scalexpert qui les transmet à Franfinance - FRANFINANCE est une société anonyme au capital de 31 357 776 euros, immatriculée au RCS de NANTERRE sous le numéro unique d'identification 719 807 406, intermédiaire en assurances - n° ORIAS 07 008 346, numéro APE : 6492Z dont le siège social se trouve au 53, rue du Port – CS 90201 – 92724 Nanterre. No TVA : FR 82 719 807 406.

&#x20;

Offre réservée aux personnes physiques majeures titulaires (résidant en France métropolitaine et DROM/COM) d’une carte bancaire valable au moins 3 mois après la date de conclusion du contrat de paiement échelonné et dont les utilisations ne sont pas soumises à une demande d’autorisation systématique (notamment les cartes Visa Electron et Maestro, pour des montants définis par le vendeur). Sous réserve d’acceptation de l’offre de paiement échelonné par Franfinance – 719 807 406 RCS Nanterre – N°ORIAS 07 008 346 ([www.orias.fr](http://www.orias.fr/)). Vous bénéficiez du délai légal de rétractation de 14 jours à compter de la date d’acceptation du contrat de paiement échelonné. Conditions au 01/11/2022.

&#x20;

Pour plus d’informations, veuillez consultez le lien suivant :

\[CHOISIR UN DES DEUX LIENS SUIVANTS SELON SI LE COMMERCANT A CHOISI LE PARTAGE DE FRAIS OU NON]

[https://opencredit.franfinance.com/docs/NXWEB-MENTIONS-3X4X-AVECFRAIS.pdf](https://opencredit.franfinance.com/docs/NXWEB-MENTIONS-3X4X-AVECFRAIS.pdf)  _(si le commerçant partage les frais)_

[https://opencredit.franfinance.com/docs/NXWEB-MENTIONS-3X4X-SANSFRAIS.pdf](https://opencredit.franfinance.com/docs/NXWEB-MENTIONS-3X4X-SANSFRAIS.pdf) _(si le commerçant prend à sa charge les frais)_

</details>
