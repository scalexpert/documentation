---
description: How to prepare data at back-end for the front snippet (optional)
---

# Snippet back-end guide (optional)

{% hint style="success" %}
Use only this guide if you choose the[ transformation from the back-end method](snippet-front-guide.md#id-3.-configuration) otherwise you don't need it.
{% endhint %}

## Scalexpert API <a href="#api-scalexpert" id="api-scalexpert"></a>

In order to display the simulation snippet with consistent data, it is necessary to call two different requests to the Scalexpert API: **Eligibility** and **Simulations** .

The compiled data from these two calls will be needed in order to build the front-end snippet.

Scalexpert documentation on both API points is available here:

* Eligibility: ![](https://3932493827-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FTpHJigxk2juo903YtJcL%2Ficon%2F58EMDyszXb3Dj1JLySB5%2Flogo_scalexpert.png?alt=media\&token=158e117b-f3eb-452c-a925-1eebdc7ed411)  [e-Financing API | Scalexpert API Docs](../../../../api-reference/e-financing-api/)
* Simulations: ![](https://3932493827-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FTpHJigxk2juo903YtJcL%2Ficon%2F58EMDyszXb3Dj1JLySB5%2Flogo_scalexpert.png?alt=media\&token=158e117b-f3eb-452c-a925-1eebdc7ed411) [e-Financing API | Scalexpert API Docs](../../../../api-reference/e-financing-api/)

### API Eligibility Point Data <a href="#donnees-du-point-dapi-eligibility" id="donnees-du-point-dapi-eligibility"></a>

This API point will already give us the available solutions depending on the merchant contract and the store context (product or cart). These solutions will be used for the simulation.

It is also necessary to retrieve the information used for display. This information is contained in the table `communicationKit`:

{% code lineNumbers="true" %}
```yaml
"visualTitle": "Payez en 3 ou 4 fois",
"visualDescription": "Baas is great",
"visualInformationIcon": "XXX/XXX.ico (url icon)",
"visualAdditionalInformation": "xxx",
"visualLegalText": "xxx",
"visualTableImage": "https://merchant.kit/uri/table.png",
"visualLogo": "https://merchant.kit/uri/productTerms.ico",
"visualInformationNoticeURL": "https://merchant.kit/uri/productTerms.pdf",
"visualProductTermsURL": "https://merchant.kit/uri/productTerms.pdf"
```
{% endcode %}

### API Point Data Simulations <a href="#donnees-du-point-dapi-simulations" id="donnees-du-point-dapi-simulations"></a>

This API point will give us digital information such as total prices, additional charges if any, the number of monthly payments and their amount.

This data will need to be formatted to display prices with decimals and currencies.\
For example, the value `solutionSimulations['simulations']['dueTotalAmount']`is `1500.0`.\
It will be necessary to change the `.`by a `,`, to add a one `0`to cents, a space to thousands and finally to suffix this price with the euro currency `€`: this will give at the end `1 500,00 €`.\
Finally, it will be necessary to add translated texts and html if necessary, to format this information.

## Front snippet <a href="#snippet-front" id="snippet-front"></a>

### Presentation <a href="#presentation" id="presentation"></a>

Following the loading of assets described in the [FRONT documentation](snippet-front-guide.md#id-3.-configuration) , a JS object`Snippet`is available.\
It is necessary to initialize it with data, you have two methods for this:

* either do it with the raw data from the Scalexpert API with the method `Snippet.setDatas`, see [FRONT Documentation | Implementation method with data returned from the raw Scalexpert API.](snippet-front-guide.md#methode-dimplementation-avec-les-donnees-retournees-de-lapi-scalexpert-brute)
* either do it with custom data (based on Scalexpert API data) with the method `Snippet.setSettings`, see [FRONT Documentation | Implementation method with data “formatted” by your solution.](snippet-front-guide.md#id-3.-configuration)\
  \
  If you decide to initialize it via the second option, here is a detailed implementation track below in order to approach the following result:

{% code overflow="wrap" lineNumbers="true" %}
```javascript
Snippet.setSettings({
    anchor: '.simulation1',
    simulations: [
        {
          title: 'Payez en 3 fois sans frais avec votre carte bancaire',
          shortDescriptionLegal: '',
          informationIconUrl: 'https://scalexpert.hml.societegenerale.com/sites/default/files/2024-02/visual_information_icon.svg',
          logoUrl: 'https://scalexpert.hml.societegenerale.com/sites/default/files/2024-02/e_financing_visual_logo_FR.svg',
          displayLogo: true,
          duration: 3,
          additionalInformation: "<p>Le paiement en 3 fois par carte bancaire est une solution de paiement qui vous permet d'échelonner le règlement de votre commande en 3 mensualités débitées sur le compte associé à votre carte bancaire.<br> Exemple : pour un achat de 600 € payé en 3 fois, vous réglez 3 échéances de 200€. Montant du financement : 600 €. TAEG FIXE: 0%. Taux débiteur fixe : 0%. Frais:0€. Montant total dû : 600€. Le prélèvement des échéances s'étale sur une durée de 90 jours maximum à compter de la date d'achat*.</p><div class='scalexpert_subtitle'>Comment ça marche ?</div><ol> <li>Ajoutez le produit à votre panier, finalisez votre achat puis validez votre panier.</li> <li>Au moment du paiement, choississez de payer en 3X avec une carte bancaire.</li> <li>Renseignez les informations demandées. Si besoin, procédez à l'authentification 3D secure, selon la méthode mise en place par votre banque. Obtenez une réponse immédiate de notre partenaire FRANFINANCE.<br>C'est terminé ! </li></ol>",
          legalText: "<div class='scalexpert_subtitle'>Conditions d'acceptation</div><p>*Offre réservée aux personnes physiques majeures titulaires (résidant en France métropolitaine et DROM/COM) d’une carte bancaire valable au moins 3 mois après la date de conclusion du contrat de paiement échelonné et dont les utilisations ne sont pas soumises à une demande d’autorisation systématique (notamment les cartes Visa Electron et Maestro, pour des montants compris entre 100 € et 4000 €).<br>Sous réserve d’acceptation de l’offre de paiement échelonné par Franfinance – 719 807 406 RCS Nanterre – N°ORIAS 07 008 346 (www.orias.fr). Vous bénéficiez du délai légal de rétractation de 14 jours à compter de la date d’acceptation du contrat de paiement échelonné. Conditions au 31/08/2023.</p>",
          infoShortDetailPayment: '<span class="scalexpert-bold">soit <span class="scalexpert-highlight">594,33 € / mois</span></span>',
          infoLongDetailPayment: 'soit <span class="scalexpert-highlight">3 prélèvements</span> de <span class="scalexpert-highlight">594,33 €</span>',
          installmentsItems: [
                '<span>Montant total dû</span><span>1 783,00 €</span>',
                '<span>Aujourd\'hui</span><span>594,33 €</span>',
                '<span>2ème prélèvement</span><span>594,33 €</span>',
                '<span>3ème prélèvement</span><span>594,34 € </span>'
          ],
          installmentsMentions: [
                'Montant du financement : 1 783,00 €.',
                'TAEG FIXE : 0%.',
                'Frais : 0,00 €.',
                'Montant total dû : 1 783,00 €.'
          ]
        },
        {
            title: 'Payez en 4 fois sans frais avec votre carte bancaire',
            shortDescriptionLegal: '',
            informationIconUrl: 'https://scalexpert.hml.societegenerale.com/sites/default/files/2024-02/visual_information_icon.svg',
            logoUrl: 'https://scalexpert.hml.societegenerale.com/sites/default/files/2024-02/e_financing_visual_logo_FR.svg',
            displayLogo: true,
            duration: 4,
            ...
        },
        ...
    ]
});
```
{% endcode %}

### Data adaptation <a href="#adaptation-des-donnees" id="adaptation-des-donnees"></a>

The index `anchor`corresponds to the Html tag on which the simulation snippet must be grafted.

The index `simulations`represents all the simulation data used to build the simulation insert.\
It is built in the form of a table compiling a dictionary of data per eligible payment solution in X times: `{Array<Object>}`.\
Here, for each index in the dictionary, is its correspondence among the API data:

| **Snippet Index**        | **Eligibility API Point Index**                                | **API Point Index Simulations**                                                                                                                                                                                                                                                                                                                                                                  | **Raw data from SG API**                                                                                                        |
| ------------------------ | -------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------- |
| `title`                  | `solutions['communicationKit']['visualTitle']`                 |                                                                                                                                                                                                                                                                                                                                                                                                  | ![check mark button](https://datasolution-group.atlassian.net/gateway/api/emoji/5d642450-16d4-4f18-b762-2678c6704a04/2705/path) |
| `shortDescriptionLegal`  | `solutions['communicationKit']['visualDescription']`           |                                                                                                                                                                                                                                                                                                                                                                                                  | ![check mark button](https://datasolution-group.atlassian.net/gateway/api/emoji/5d642450-16d4-4f18-b762-2678c6704a04/2705/path) |
| `informationIconUrl`     | `solutions['communicationKit']['visualInformationIcon']`       |                                                                                                                                                                                                                                                                                                                                                                                                  | ![check mark button](https://datasolution-group.atlassian.net/gateway/api/emoji/5d642450-16d4-4f18-b762-2678c6704a04/2705/path) |
| `logoUrl`                | `solutions['communicationKit']['visualLogo']`                  |                                                                                                                                                                                                                                                                                                                                                                                                  | ![check mark button](https://datasolution-group.atlassian.net/gateway/api/emoji/5d642450-16d4-4f18-b762-2678c6704a04/2705/path) |
| `duration`               |                                                                | `solutionSimulations['simulations']['duration']`                                                                                                                                                                                                                                                                                                                                                 | ![check mark button](https://datasolution-group.atlassian.net/gateway/api/emoji/5d642450-16d4-4f18-b762-2678c6704a04/2705/path) |
| `additionalInformation`  | `solutions['communicationKit']['visualAdditionalInformation']` |                                                                                                                                                                                                                                                                                                                                                                                                  | ![check mark button](https://datasolution-group.atlassian.net/gateway/api/emoji/5d642450-16d4-4f18-b762-2678c6704a04/2705/path) |
| `legalText`              | `solutions['communicationKit']['visualLegalText']`             |                                                                                                                                                                                                                                                                                                                                                                                                  | ![check mark button](https://datasolution-group.atlassian.net/gateway/api/emoji/5d642450-16d4-4f18-b762-2678c6704a04/2705/path) |
| `infoShortDetailPayment` |                                                                | `solutionSimulations['simulations']['installments']['amount']`                                                                                                                                                                                                                                                                                                                                   |                                                                                                                                 |
| `infoLongDetailPayment`  |                                                                | `solutionSimulations['simulations']['duration']`+`solutionSimulations['simulations']['installments']['amount']`                                                                                                                                                                                                                                                                                  |                                                                                                                                 |
| `installmentsItems`      |                                                                | `solutionSimulations['simulations']['dueTotalAmount']`+ `solutionSimulations['simulations']['duration']`+`solutionSimulations['simulations']['installments']['amount']`                                                                                                                                                                                                                          |                                                                                                                                 |
| `installmentsMentions`   |                                                                | <p><code>financedAmount</code>+<br><code>solutionSimulations['simulations']['dueTotalAmount']</code>+ <code>solutionSimulations['simulations']['effectiveAnnualPercentageRate']</code>+ <code>solutionSimulations['simulations']['nominalPercentageRate']</code>+ <code>solutionSimulations['simulations']['totalCost']</code>+<code>solutionSimulations['simulations']['feesAmount']</code></p> |                                                                                                                                 |

We can therefore see that for certain indexes, we can recover the value returned by the API as it is, while for others it will be necessary to format and complete the data with text and html as explained previously (cf. BACK [Documentation | Simulations API Point Data](../../../../solutions-reference/credit/) ).

\
For the indexes `infoShortDetailPayment`and `infoLongDetailPayment`, we use the price entered in `solutionSimulations['simulations']['installments']['amount']`and if necessary the number of monthly payments in `solutionSimulations['simulations']['duration']`.\
It should be noted that, for financing solutions including additional costs, it will be wise to display the monthly payments for the first two months, in order to have visibility on a monthly payment including costs and then on a classic monthly payment.

{% code lineNumbers="true" %}
```php
infoShortDetailPayment: '<span class="scalexpert-bold">soit un 1er prélèvement de <span class="scalexpert-highlight">465,75 €</span> (frais inclus) puis 3 prélèvements de <span class="scalexpert-highlight">445,75 €</span></span>',
infoLongDetailPayment: 'soit un <span class="scalexpert-highlight">1er prélèvement</span> de <span class="scalexpert-highlight">465,75 €</span> (frais inclus) puis <span class="scalexpert-highlight">3 prélèvements</span> de <span class="scalexpert-highlight">445,75 €</span>'
```
{% endcode %}

&#x20;

For the `installmentsItems`and indexes `installmentsMentions`, it is about creating a table of strings (including html or not) that will be displayed in the modal window of the snippet.\
The idea is therefore also to base itself on the data from the different API points, to format them and then to combine them with translated texts in order to build a table with an entry per monthly payment for the index `installmentsItems`and a table with all the fees and percentages specific to the financing solution chosen for the index `installmentsMentions`.

{% code lineNumbers="true" %}
```php
installmentsItems: [
    solutionSimulations['simulations']['installments'][0]['amount'],
    solutionSimulations['simulations']['installments'][1]['amount'],
    solutionSimulations['simulations']['installments'][2]['amount'],
    solutionSimulations['simulations']['installments'][3]['amount'],
    ...
],
installmentsMentions: [
    financedAmount,
    solutionSimulations['simulations']['effectiveAnnualPercentageRate'],
    solutionSimulations['simulations']['feesAmount'],
    solutionSimulations['simulations']['dueTotalAmount']
]
```
{% endcode %}

### Examples of data transformation <a href="#exemples-de-transformation-des-donnees" id="exemples-de-transformation-des-donnees"></a>

Here are examples of modifying the data here from the API, in order to stick to what is expected by the snippet for display.\
The following examples are therefore made in JavaScript.

Price formatting:

{% code lineNumbers="true" %}
```php
const buyerBillingCountry = 'FR';
const currencies = {
    'US': { code: "USD", locale: "en-US" },
    'FR': { code: "EUR", locale: "fr-FR" },
}
const currencyFormatter = new Intl.NumberFormat(currencies[buyerBillingCountry].locale, {
    style: 'currency',
    currency: currencies[buyerBillingCountry].code,
});

let financedAmountFormatted = currencyFormatter.format(1500.00);
```
{% endcode %}

Formatting percentages:

{% code lineNumbers="true" %}
```php
const formatPercent = (percent) => `${percent.toFixed(2)} %`;
let percentageRateFormatted = formatPercent(0.25);
```
{% endcode %}

And here is a complete example of a method that aims to format the data of the simulation API point:

{% code lineNumbers="true" %}
```php
/**
* La méthode prepareData prend en paramètre la réponse du point API Simulation
*/
function prepareSimulationData(dataFromAPI) {
      // Liste des codes solutions possédant des frais supplémentaires
      const feesSolutions = [
          'SCFRSP-3XPS',
          'SCFRSP-4XPS',
          'SCFRLT-TXPS',
      ];
      // Liste des codes solutions faisant partie des financement de longue durée
      const longSolutions = [
          'SCFRLT-TXPS',
          'SCFRLT-TXNO',
          'SCDELT-DXTS',
          'SCDELT-DXCO',
      ];
      
      // Fonction de formatage des prix
      const currencies = {
          'US': { code: "USD", locale: "en-US" },
          'FR': { code: "EUR", locale: "fr-FR" },
      }
      const currencyFormatter = new Intl.NumberFormat(currencies[dataFromAPI.buyerBillingCountry].locale, {
          style: 'currency',
          currency: currencies[dataFromAPI.buyerBillingCountry].code,
      });
      
      // Fonction de formatage des pourcentages
      const formatPercent = (percent) => `${percent.toFixed(2)} %`;

      let preparedData = [];
      for (const i in dataFromAPI.solutionSimulations) {
          for (const j in dataFromAPI.solutionSimulations[i].simulations) {
              const solutionCode = dataFromAPI.solutionSimulations[i].solutionCode;
              const isLongFinancingSolution = longSolutions.includes(solutionCode);
              const hasFeesOnFirstInstallment = feesSolutions.includes(solutionCode);
              
              let simulationData = {
                  title: '',
                  displayLogo: true,
                  duration: dataFromAPI.solutionSimulations[i].simulations[j].duration,
                  ... // Données à récupérer du point d'API /eligible-solutions
                  installmentsItems: [
                    `<span>Montant total dû</span><span>${currencyFormatter.format(dataFromAPI.solutionSimulations[i].simulations[j].dueTotalAmount)}</span>`
                  ],
                  installmentsMentions: [
                    `Montant du financement : ${currencyFormatter.format(data.financedAmount)}.`,
                    `TAEG FIXE : ${formatPercent(dataFromAPI.solutionSimulations[i].simulations[j].effectiveAnnualPercentageRate)}.`,
                    `Frais : ${currencyFormatter.format(dataFromAPI.solutionSimulations[i].simulations[j].feesAmount)}.`,
                    `Montant total dû : ${currencyFormatter.format(dataFromAPI.solutionSimulations[i].simulations[j].dueTotalAmount)}.`
                  ]
              };
              
              const feesLabel = (hasFeesOnFirstInstallment) ? 'avec frais' : 'sans frais';
              simulationData.title = `Payez en ${simulationData.duration} fois ${feesLabel} avec votre carte bancaire`;

              for (const k in dataFromAPI.solutionSimulations[i].simulations[j].installments) {
                  const number = dataFromAPI.solutionSimulations[i].simulations[j].installments[k].number;
                  const numberLabel = (1 === number) ? 'Aujourd\'hui' : `${number}ème prélèvement`;

                  simulationData.installmentsItems.push(`<span>${numberLabel}</span><span>${currencyFormatter.format(dataFromAPI.solutionSimulations[i].simulations[j].installments[k].amount)}</span>`););
              }

              preparedData.push(simulationData);
          }
      }

      // Sort by duration
      preparedData.sort((a, b) => a.duration - b.duration);

      return preparedData;
  }
```
{% endcode %}

&#x20;

\
