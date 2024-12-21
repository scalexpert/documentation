---
description: Describe the way to onboard a seller through MS API
---

# Seller onboarding

First of all, to start working with Marketplace Services, you have to integrate a set of endpoints to onboard your sellers. These endpoint are designed to support the onboarding in multiple-times without having to save any sensitive data on your side.

## Onboarding & KYB endpoints: <a href="#onboarding-and-kyb-endpoints" id="onboarding-and-kyb-endpoints"></a>

| **HTTP request** | **Endpoint** | **Usage** |
| ---------------- | ------------ | --------- |

| **HTTP request** | **Endpoint**                                                           | **Usage**                                                                                   |
| ---------------- | ---------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| PUT              | /sellers/{merchantSellerId}                                            | Start the onboarding of a seller based on your own id.                                      |
| GET              | /sellers/{merchantSellerId}                                            | Get all values already filled of a seller                                                   |
| POST             | /sellers/{merchantSellerId}/contacts                                   | Add a physical person on a existing seller. All effective beneficiaries must be added.      |
| PATCH            | /sellers/{merchantSellerId}/contacts/{contactId}                       | Change some informations about a contact                                                    |
| DELETE           | /sellers/{merchantSellerId}/contacts/{contactId}                       | Delete a contact                                                                            |
| POST             | /sellers/{merchantSellerId}/documents                                  | Add a document attached to a seller (KBIS, fiscal statement, etc.)                          |
| DELETE           | /sellers/{merchantSellerId}/documents/{documentId}                     | Delete a seller document                                                                    |
| POST             | /sellers/{merchantSellerId}/contact/{contactId}/documents              | Add a document attached to an effective beneficiary (Id card, passport, etc.)               |
| DELETE           | /sellers/{merchantSellerId}/contact/{contactId}/documents/{documentId} | Delete a contact document                                                                   |
| POST             | /sellers/{merchantSellerId}/\_assess-kyc                               | Start the KYB of a specific seller and all the KYC of the contacts attached to this seller. |

## Onboarding & KYB journey <a href="#onboarding-and-kyb-journey" id="onboarding-and-kyb-journey"></a>

**Objective: launch the KYB review of a seller**

### 1 - Manage the sellers <a href="#id-1-manage-the-sellers" id="id-1-manage-the-sellers"></a>

The solution is designed to allow the marketplace to use his own ID to manage the sellers in the scaleXpert environement.

For an existing seller, the marketplace make a KYB renewal for the seller. Some fields already known by the marketplace and could be pre-filled.

Pre-requisite to call the API endpoint

* You have a solutionCode
* You have the right credentials

&#x20;

The seller is connected to the markeptlace back-office and is in the registration process. Different forms (depending your own design) allow the seller to complete required informations. Each time a new data is filled, the marketplace can use the endpoint `PUT /sellers/{merchantSellerId}` to store the values filled.

If the values are not registered on the marketplace side, and the seller comes somes days after to add some new informations, the marketplace can retreive all th previous stored datas with the request: `GET /sellers/{merchantSellerId}`

### 2 - Manage the contacts <a href="#id-2-manage-the-contacts" id="id-2-manage-the-contacts"></a>

After the seller creation, the marketplace can add all the contacts required. Here the contacts are all the direct and indirect UBO of the seller.

To know the criterias of an Ultimate Beneficiary Owner (UBO) of a company: [RBE\_Fiche\_pratique\_schemas (greffe-tc-paris.fr)](https://www.greffe-tc-paris.fr/uploads/paris/Fiches%20RCS/RBE_Fiche_pratique_schemas.pdf)&#x20;

The HTTP verbs availables to manage contacts are the classicals POST, PATCH and DELETE with the standard rules of the rest protocol.

### &#x20;3 - Manage the documents

In order to process the KYB of the seller and each contacts, the marketplace must ask to the seller several documents. A document cannot be updated but only added or deleted.

At minimum you have to provide for each seller the kBis of the company and for each attached contact a proof of identity (CNI or passeport)

The available methods allow to post as many documents as necessary on a seller and on a contact.

### 4 - Launch the KYB of the seller <a href="#id-4-launch-the-kyb-of-the-seller" id="id-4-launch-the-kyb-of-the-seller"></a>

The marketplace should allow the seller to launch the KYB process with an explicit button.

As soon as the seller has filled at a minimum:

* Required fields of the seller endpoint
* One attached document
* One contact as minimum
* Required fileds of the contact endpoint
* One document attached to the contact as minimum

The endpoint "\[...]/\_assess-kyc" is now available and the seller can launch the KYB process.

{% hint style="info" %}
As soon as the endpoint is called, the seller and all attached contacts and documents are no more updatable. THe KYC review take around 48 hours. The marketpalace should wait for the status change (webhook) to know if some changes are required or if the seller KYB is ACCEPTED.
{% endhint %}





**List of the Webhooks TBC**

**List of error codes**

**Seller lifecycle ?**

