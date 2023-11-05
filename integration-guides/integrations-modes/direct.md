---
description: How to integrate our solutions with APIs
---

# APIs

## API Integration Guide

### Table of Contents

1. Introduction
2. API Overview
3. Getting Started
4. API Integration Steps
5. Best Practices and Considerations
6. Troubleshooting and Support

{% hint style="info" %}
In this guide you will find snippets for Node.js, Java, PHP and Python server langages.
{% endhint %}

### 1. Introduction

This API integration guide will walk you through the process of setting up your environments so you can later consume scalexpert APIs into your application or platform.

By integrating these APIs, you'll be able to initiate and manage e-financing subscriptions on behalf of your customers or dynamically propose warranty extensions for some items on their basket prior checkout.

### 2. API Overview

The APIs allows you to interact with the our platform pro-grammatically, enabling you to initiate and manage financing or insurance proposals seamlessly. Here are some key aspects of the APIs:

* RESTful architecture: Utilize standard HTTP methods (GET, POST, PUT, DELETE) to interact with the API.
* JSON-based data format: Send and receive data in JSON format, ensuring compatibility and ease of integration across different programming languages.
* oAuth2 client credentials authentication flow (server to server).

For more details refer to:

{% content-ref url="../../api-reference/apis-common/" %}
[apis-common](../../api-reference/apis-common/)
{% endcontent-ref %}

#### Authentication and Authorization

To access these APIs, you'll need to authenticate your requests by obtaining [an oAuth2 access token](direct.md#obtain-an-oauth2-access-token). API Keys are obtained from the developer portal, which serves as your access credential. They are used to authenticate your service using [**oAuth 2.0 client credentials flow.**](../../api-reference/apis-common/authentication.md) Upon authorization for the claimed scopes the issued token will be used to identify each subsequent request.

Refer to authentication API reference for more details:

{% content-ref url="../../api-reference/apis-common/authentication.md" %}
[authentication.md](../../api-reference/apis-common/authentication.md)
{% endcontent-ref %}

#### Obtain an oAuth2 access token

{% tabs %}
{% tab title="Node.js" %}
{% code title="Node.js native" overflow="wrap" lineNumbers="true" fullWidth="true" %}
```n4js
var https = require('follow-redirects').https;
var fs = require('fs');

var qs = require('querystring');

var options = {
  'method': 'POST',
  'hostname': 'api.e-commerce.societegenerale.com',
  'path': '/baas/prod/auth-server/api/v1/oauth2/token',
  'headers': {
    'Content-Type': 'application/x-www-form-urlencoded',
    'Authorization': 'Basic ZmU3ZmVmYjktNmEyZ...zdqQW89'
  },
  'maxRedirects': 20
};

var req = https.request(options, function (res) {
  var chunks = [];

  res.on("data", function (chunk) {
    chunks.push(chunk);
  });

  res.on("end", function (chunk) {
    var body = Buffer.concat(chunks);
    console.log(body.toString());
  });

  res.on("error", function (error) {
    console.error(error);
  });
});

var postData = qs.stringify({
  'grant_type': 'client_credentials',
  'scope': 'e-financing:rw'
});

req.write(postData);

req.end();
```
{% endcode %}
{% endtab %}

{% tab title="PHP" %}
{% code title="PHP - HTTP2_request2" overflow="wrap" lineNumbers="true" fullWidth="true" %}
```php
<?php
require_once 'HTTP/Request2.php';
$request = new HTTP_Request2();
$request->setUrl('https://api.e-commerce.societegenerale.com/baas/prod/auth-server/api/v1/oauth2/token');
$request->setMethod(HTTP_Request2::METHOD_POST);
$request->setConfig(array(
  'follow_redirects' => TRUE
));
$request->setHeader(array(
  'Content-Type' => 'application/x-www-form-urlencoded',
  'Authorization' => 'Basic ZmU3ZmVmYjktNmEyZS00YjcyLWI4MzAtMGJlMTMxZTFkZTdhOnVsRmpNc29yejJoekZWM1EvQng4RldaSk41aG1BNk95WGFIQVdLSzdqQW89'
));
$request->addPostParameter(array(
  'grant_type' => 'client_credentials',
  'scope' => 'e-financing:rw'
));
try {
  $response = $request->send();
  if ($response->getStatus() == 200) {
    echo $response->getBody();
  }
  else {
    echo 'Unexpected HTTP status: ' . $response->getStatus() . ' ' .
    $response->getReasonPhrase();
  }
}
catch(HTTP_Request2_Exception $e) {
  echo 'Error: ' . $e->getMessage();
}
```
{% endcode %}
{% endtab %}

{% tab title="Java" %}
{% code title="Java - OKHttp" overflow="wrap" lineNumbers="true" fullWidth="true" %}
```java
OkHttpClient client = new OkHttpClient().newBuilder()
  .build();
MediaType mediaType = MediaType.parse("application/x-www-form-urlencoded");
RequestBody body = RequestBody.create(mediaType, "grant_type=client_credentials&scope=e-financing:rw");
Request request = new Request.Builder()
  .url("https://api.e-commerce.societegenerale.com/baas/prod/auth-server/api/v1/oauth2/token")
  .method("POST", body)
  .addHeader("Content-Type", "application/x-www-form-urlencoded")
  .addHeader("Authorization", "Basic ZmU3ZmVmYjktNmEyZS00YjcyLWI4MzAtMGJlMTMxZTFkZTdhOnVsRmpNc29yejJoekZWM1EvQng4RldaSk41aG1BNk95WGFIQVdLSzdqQW89")
  .build();
Response response = client.newCall(request).execute();
```
{% endcode %}
{% endtab %}

{% tab title="Python" %}
{% code title="Python request" overflow="wrap" lineNumbers="true" %}
```python
import requests

url = "https://api.scalexpert.uatc.societegenerale.com/baas/uatc/auth-server/api/v1/oauth2/token/oauth2/token"

payload = 'grant_type=client_credentials&scope=e-financing%3Arw'
headers = {
  'Content-Type': 'application/x-www-form-urlencoded',
  'Authorization': 'Basic ZmU3ZmVm...tRcnc9'
}

response = requests.request("POST", url, headers=headers, data=payload)

print(response.text)
```
{% endcode %}
{% endtab %}
{% endtabs %}

#### API Endpoints and Request/Response Formats

The API provides various endpoints for managing subscriptions or retrieving relevant data. Each endpoint supports specific actions and requires specific parameters. Requests should include appropriate headers, and responses are returned in JSON format.

Refer to the **API reference** section for detailed information on each endpoint, including request/response examples and required parameters.

{% content-ref url="broken-reference" %}
[Broken link](broken-reference)
{% endcontent-ref %}

### 3. Getting Started

#### Prerequisites for Integration

Before starting the integration process, make sure you have complete the prerequisites. Refer to "Before you start" pages for more details

{% content-ref url="../../ready-to-start/before-you-start/" %}
[before-you-start](../../ready-to-start/before-you-start/)
{% endcontent-ref %}

Also have a look at "Security best practices" pages. For instance, make attention that API must be implemented at server side and not at front side.

{% content-ref url="../../security/security-best-practices.md" %}
[security-best-practices.md](../../security/security-best-practices.md)
{% endcontent-ref %}

#### API Access Credentials and Keys

Refer to "Before you start/API key" section for instructions:

{% content-ref url="../../ready-to-start/before-you-start/api-key.md" %}
[api-key.md](../../ready-to-start/before-you-start/api-key.md)
{% endcontent-ref %}

#### Testing Environment Setup

Set up a testing environment to ensure smooth integration and testing of the E-Financing API:

* [User Acceptance Test for customer (UATC) ](../../api-reference/apis-common/api-urls.md#test-for-customer-uatc)environment that will simulates the production environment. Use this environment for development, integration, and testing purposes.
* API Documentation: Familiarize yourself with the API documentation, including endpoint details, request/response examples, and any available snippets  that can expedite the integration process.

### 4. API Integration Steps

Now let's dive into the steps involved in integrating the **E-Financing** API into your application or platform:

#### Step 1: Check Eligible E-Financing Solutions

To determine the eligible e-financing solutions available for a specific purchase, follow these steps:

1. Collect Purchase Information: Gather relevant purchase details, such as the total amount and country of the buyer end user (or by default country of your site).
2. Make a GET Request: Utilize the API endpoint responsible for checking eligibility, passing the necessary purchase information.
3. Handle Response: Capture and process the response, which will indicate the available e-financing solutions and their associated merchant communication kit informations.
4. According the response render the solution to end users for instance on product page by showcasing the solutions (see next step).&#x20;

Refer to [API GET /eligible-solutions](../../api-reference/e-financing-api/)

{% tabs %}
{% tab title="Node.js" %}
{% code title="Node.js native" overflow="wrap" lineNumbers="true" fullWidth="true" %}
```n4js
var https = require('follow-redirects').https;
var fs = require('fs');

var options = {
  'method': 'GET',
  'hostname': 'api.scalexpert.uatc.societegenerale.com',
  'path': '/baas/uatc/e-financing/api/v1/eligible-solutions?financedAmount=500&buyerBillingCountry=FR',
  'headers': {
    'Authorization': 'Bearer eyJlbmMiOi...TxWr8u9ooNMZ3zI'
  },
  'maxRedirects': 20
};

var req = https.request(options, function (res) {
  var chunks = [];

  res.on("data", function (chunk) {
    chunks.push(chunk);
  });

  res.on("end", function (chunk) {
    var body = Buffer.concat(chunks);
    console.log(body.toString());
  });

  res.on("error", function (error) {
    console.error(error);
  });
});

req.end();
```
{% endcode %}
{% endtab %}

{% tab title="PHP" %}
{% code title="PHP - HTTP_request2" overflow="wrap" lineNumbers="true" %}
```php
<?php
require_once 'HTTP/Request2.php';
$request = new HTTP_Request2();
$request->setUrl('https://api.scalexpert.uatc.societegenerale.com/baas/uatc/e-financing/api/v1/eligible-solutions?financedAmount=500&buyerBillingCountry=FR');
$request->setMethod(HTTP_Request2::METHOD_GET);
$request->setConfig(array(
  'follow_redirects' => TRUE
));
$request->setHeader(array(
  'Authorization' => 'Bearer eyJlbmMiOiJBMjU2Q0JDLUhTNT...TxWr8u9ooNMZ3zI'
));
try {
  $response = $request->send();
  if ($response->getStatus() == 200) {
    echo $response->getBody();
  }
  else {
    echo 'Unexpected HTTP status: ' . $response->getStatus() . ' ' .
    $response->getReasonPhrase();
  }
}
catch(HTTP_Request2_Exception $e) {
  echo 'Error: ' . $e->getMessage();
}
```
{% endcode %}
{% endtab %}

{% tab title="Java" %}
{% code title="Java - OKHttp" overflow="wrap" lineNumbers="true" %}
```java
OkHttpClient client = new OkHttpClient().newBuilder()
  .build();
MediaType mediaType = MediaType.parse("text/plain");
RequestBody body = RequestBody.create(mediaType, "");
Request request = new Request.Builder()
  .url("https://api.scalexpert.uatc.societegenerale.com/baas/uatc/e-financing/api/v1/eligible-solutions?financedAmount=500&buyerBillingCountry=FR")
  .method("GET", body)
  .addHeader("Authorization", "Bearer eyJlbmMiOiJBMjU2Q0JDLUhTN...Wr8u9ooNMZ3zI")
  .build();
Response response = client.newCall(request).execute();
```
{% endcode %}
{% endtab %}

{% tab title="Python" %}
{% code title="Python request" overflow="wrap" lineNumbers="true" %}
```python
import requests

url = "https://api.scalexpert.uatc.societegenerale.com/baas/uatc/e-financing/api/v1/eligible-solutions?financedAmount=1000&buyerBillingCountry=FR"

payload = {}
headers = {
  'Authorization': 'Bearer eyJlbmMiOiJBMjU2Q0JDLUhTNTEyIiwiYWxnIjoiQTI1NktXIn0.ftNiQraQFkH9i0oHOCGXZ465HxD8-lEzdPfczpGVWMk04zY...Fzgpmok-aK9ljGv7cM8'
}

response = requests.request("GET", url, headers=headers, data=payload)

print(response.text)

```
{% endcode %}
{% endtab %}
{% endtabs %}

#### Step 2: Showcasing the solutions

By "showcasing solutions" we mean rendering the solutions at product or checkout pages (see more details [here](../../for-discovery/showcasing-solutions.md)). This will be possible with the response of [GET /eligible-solutions](../../api-reference/e-financing-api/) and object "`communicationKit`" and its attributes that contains texts with HTML, logos, images ...

{% code title="Response GET /eligible-solutions" overflow="wrap" %}
````json
{
    "solutions": [
        {
            "solutionCode": "SCFRLT-TXNO",
            "familyCode": "SC",
            "marketCode": "FR",
            "conditions": "PS",
            "communicationKit": {
                "solutionCode": "SCFRLT-TXNO",
                "visualTitle": "<div class=scalexpert_title>Etalez votre paiment avec un crédit</div>",
                "visualDescription": "Un crédit vous engage et doit être remboursé. Vérifiez vos capacités de remboursement avant de vous engager.",
                "visualInformationIcon": "https://scalexpert.societegenerale.com/app/merchantKit/visual_information_icon.svg",
                "visualAdditionalInformation": "<div class=scalexpert_subtitle>Comment ça marche ?</div><ol> <li>Ajoutez le produit à votre panier et finalisez votre achat. Validez votre panier</li> <li>Au moment du paiement, choisissez d'étaler votre paiement avec un crédit.</li> <li>Renseignez les informations demandées, munissez-vous de votre pièce d'identité et signez électroniquement votre contrat de financement. Obtenez une réponse immédiate de notre partenaire FRANFINANCE. <br>C'est terminé! </li></ol>",
                "visualLegalText": "<div class=scalexpert_subtitle>Mentions légales</div><p>Un crédit vous engage et doit être remboursé. Vérifiez vos capacités de remboursement avant de vous engager. Offre valable toute l’année, à partir de 1000 euros de crédit et sous réserve d’acceptation du crédit affecté par FRANFINANCE (SA au capital de 31.357.776,00 euros - 719 807 406 RCS Nanterre - 53 rue du Port, CS 90201, 92724 Nanterre Cedex - France -, Intermédiaire en assurance inscrit l’ORIAS N° 07 008 346 - www.orias.fr). Vous disposez d’un délai de rétractation de 14 jours à compter de la date de signature du contrat de crédit. Le vendeur est intermédiaire de crédit non exclusif de FRANFINANCE, immatriculé à l’ORIAS sous le numéro XXXXX (www.orias.fr).</p>",
                "visualTableImage": null,
                "visualLogo": "https://scalexpert.societegenerale.com/app/merchantKit/e_financing_visual_logo_FR.svg",
                "visualInformationNoticeURL": null,
                "visualProductTermsURL": null
            }
        },
```
````
{% endcode %}

Rendering of communication KIT (ex long term credit):

<figure><img src="../../.gitbook/assets/Capture d’écran du 2023-11-05 16-28-52.png" alt="" width="375"><figcaption><p>Communication Kit rendering</p></figcaption></figure>

{% hint style="warning" %}
Make sure at minimum "visualLegalText" is always rendered on your site for legal compliance.
{% endhint %}

#### Step 3: Initiate an E-Financing Subscription

To initiate an e-financing subscription for a customer, follow these steps:

1. Collect Customer Information: Gather the required customer information, such as name, contact details, and billing address.
2. Make a POST Request: Use the appropriate API endpoint, passing the necessary customer information and subscription details.
3. Handle Response: Capture and process the response, which will contain the subscription ID and any additional information provided by the API.

Refer to [API POST /susbscriptions](../../api-reference/e-financing-api/)

{% tabs %}
{% tab title="Node.js" %}
{% code title="Node.js - Native" overflow="wrap" lineNumbers="true" %}
```n4js
var https = require('follow-redirects').https;
var fs = require('fs');

var options = {
  'method': 'POST',
  'hostname': 'api.e-commerce.uatc.societegenerale.com',
  'path': '/baas/uatc/e-financing/api/v1/subscriptions',
  'headers': {
    'Content-Type': 'application/json',
    'Authorization': 'Bearer eyJlbmMiOiJBMjU2Q0J...u9ooNMZ3zI'
  },
  'maxRedirects': 20
};

var req = https.request(options, function (res) {
  var chunks = [];

  res.on("data", function (chunk) {
    chunks.push(chunk);
  });

  res.on("end", function (chunk) {
    var body = Buffer.concat(chunks);
    console.log(body.toString());
  });

  res.on("error", function (error) {
    console.error(error);
  });
});

var postData = JSON.stringify({
  "financedAmount": 119.9,
  "solutionCode": "SCFRSP-4XTS",
  "merchantBasketId": "647aeb24-a89c-11ed-afa1-0242ac120002",
  "merchantGlobalOrderId": "XbB6_sMPbkvRk0y#206578",
  "merchantBuyerId": "701943",
  "merchantUrls": {
    "confirmation": "https://mymerchand.domain/uri"
  },
  "buyers": [
    {
      "billingContact": {
        "lastName": "Dupont",
        "firstName": "Paul",
        "commonTitle": "Mr.",
        "email": "paul.dupont@mail.com",
        "mobilePhoneNumber": "+33684749393",
        "professionalTitle": "Professor",
        "phoneNumber": "+33184749393"
      },
      "billingAddress": {
        "locationType": "billingAddress",
        "streetNumber": 147,
        "streetNumberSuffix": "B",
        "streetName": "main street",
        "streetNameComplement": "block 47",
        "zipCode": "92060",
        "cityName": "Paris",
        "regionName": "Île-de-France",
        "countryCode": "FR"
      },
      "deliveryContact": {
        "lastName": "Dupont",
        "firstName": "Paul",
        "commonTitle": "Mr.",
        "email": "paul.dupont@mail.com",
        "mobilePhoneNumber": "+33684749393",
        "professionalTitle": "Professor",
        "phoneNumber": "+33184749393"
      },
      "deliveryAddress": {
        "locationType": "billingAddress",
        "streetNumber": 147,
        "streetNumberSuffix": "B",
        "streetName": "main street",
        "streetNameComplement": "block 47",
        "zipCode": "92060",
        "cityName": "Paris",
        "regionName": "Île-de-France",
        "countryCode": "FR"
      },
      "contact": {
        "lastName": "Dupont",
        "firstName": "P",
        "commonTitle": "Mr.",
        "email": "paul.dupont@mail.com",
        "mobilePhoneNumber": "+33684749393",
        "professionalTitle": "Professor",
        "phoneNumber": "+33184749393"
      },
      "contactAddress": {
        "locationType": "billingAddress",
        "streetNumber": 147,
        "streetNumberSuffix": "B",
        "streetName": "main street",
        "streetNameComplement": "block 47",
        "zipCode": "92060",
        "cityName": "Paris",
        "regionName": "Île-de-France",
        "countryCode": "FR"
      },
      "deliveryMethod": "Click & Collect",
      "birthName": "Dupont",
      "birthDate": "01021975",
      "birthCityName": "Montpellier",
      "birthCountryName": "FR",
      "vip": false
    }
  ],
  "basketDetails": {
    "basketItems": [
      {
        "id": "M12345785513211",
        "quantity": 2,
        "model": "5KPM5",
        "label": "PANTALON B MAGO",
        "price": 9500,
        "currencyCode": "EUR",
        "orderId": "OD456742",
        "brandName": "KitchenAid",
        "description": "Le robot pâtissier à bol relevable très résistant idéal pour mixer de grandes quantités d'ingrédients, équipé d'un bol en acier inoxydable amovible.",
        "specifications": "Puissance (W) 315, Tension (V) 220-240, Fréquence (Hz) 50/60",
        "category": "R78757857",
        "isFinanced": true,
        "sku": "50"
      }
    ]
  }
});

req.write(postData);

req.end();
```
{% endcode %}
{% endtab %}

{% tab title="PHP" %}
{% code title="PHP - Http_Request2" overflow="wrap" lineNumbers="true" %}
```php
<?php
require_once 'HTTP/Request2.php';
$request = new HTTP_Request2();
$request->setUrl('https://api.e-commerce.uatc.societegenerale.com/baas/uatc/e-financing/api/v1/subscriptions');
$request->setMethod(HTTP_Request2::METHOD_POST);
$request->setConfig(array(
  'follow_redirects' => TRUE
));
$request->setHeader(array(
  'Content-Type' => 'application/json',
  'Authorization' => 'Bearer eyJlbmMiOiJBMjU2Q0JDLUh...- -_Request28u9ooNMZ3zI'
));
$request->setBody('{
\n    "financedAmount": 119.9,
\n    "solutionCode": "SCFRSP-4XTS",
\n    "merchantBasketId": "647aeb24-a89c-11ed-afa1-0242ac120002",
\n    "merchantGlobalOrderId": "XbB6_sMPbkvRk0y#206578",
\n    "merchantBuyerId": "701943",
\n    "merchantUrls": {
\n        "confirmation": "https://mymerchand.domain/uri"
\n    },
\n    "buyers": [
\n        {
\n            "billingContact": {
\n                "lastName": "Dupont",
\n                "firstName": "Paul",
\n                "commonTitle": "Mr.",
\n                "email": "paul.dupont@mail.com",
\n                "mobilePhoneNumber": "+33684749393",
\n                "professionalTitle": "Professor",
\n                "phoneNumber": "+33184749393"
\n            },
\n            "billingAddress": {
\n                "locationType": "billingAddress",
\n                "streetNumber": 147,
\n                "streetNumberSuffix": "B",
\n                "streetName": "main street",
\n                "streetNameComplement": "block 47",
\n                "zipCode": "92060",
\n                "cityName": "Paris",
\n                "regionName": "Île-de-France",
\n                "countryCode": "FR"
\n            },
\n            "deliveryContact": {
\n                "lastName": "Dupont",
\n                "firstName": "Paul",
\n                "commonTitle": "Mr.",
\n                "email": "paul.dupont@mail.com",
\n                "mobilePhoneNumber": "+33684749393",
\n                "professionalTitle": "Professor",
\n                "phoneNumber": "+33184749393"
\n            },
\n            "deliveryAddress": {
\n                "locationType": "billingAddress",
\n                "streetNumber": 147,
\n                "streetNumberSuffix": "B",
\n                "streetName": "main street",
\n                "streetNameComplement": "block 47",
\n                "zipCode": "92060",
\n                "cityName": "Paris",
\n                "regionName": "Île-de-France",
\n                "countryCode": "FR"
\n            },
\n            "contact": {
\n                "lastName": "Dupont",
\n                "firstName": "P",
\n                "commonTitle": "Mr.",
\n                "email": "paul.dupont@mail.com",
\n                "mobilePhoneNumber": "+33684749393",
\n                "professionalTitle": "Professor",
\n                "phoneNumber": "+33184749393"
\n            },
\n            "contactAddress": {
\n                "locationType": "billingAddress",
\n                "streetNumber": 147,
\n                "streetNumberSuffix": "B",
\n                "streetName": "main street",
\n                "streetNameComplement": "block 47",
\n                "zipCode": "92060",
\n                "cityName": "Paris",
\n                "regionName": "Île-de-France",
\n                "countryCode": "FR"
\n            },
\n            "deliveryMethod": "Click & Collect",
\n            "birthName": "Dupont",
\n            "birthDate": "01021975",
\n            "birthCityName": "Montpellier",
\n            "birthCountryName": "FR",
\n            "vip": false
\n        }
\n    ],
\n    "basketDetails": {
\n        "basketItems": [
\n            {
\n                "id": "M12345785513211",
\n                "quantity": 2,
\n                "model": "5KPM5",
\n                "label": "PANTALON B MAGO",
\n                "price": 9500,
\n                "currencyCode": "EUR",
\n                "orderId": "OD456742",
\n                "brandName": "KitchenAid",
\n                "description": "Le robot pâtissier à bol relevable très résistant idéal pour mixer de grandes quantités d\'ingrédients, équipé d\'un bol en acier inoxydable amovible.",
\n                "specifications": "Puissance (W) 315, Tension (V) 220-240, Fréquence (Hz) 50/60",
\n                "category": "R78757857",
\n                "isFinanced": true,
\n                "sku": "50"
\n            }
\n        ]
\n    }
\n}');
try {
  $response = $request->send();
  if ($response->getStatus() == 200) {
    echo $response->getBody();
  }
  else {
    echo 'Unexpected HTTP status: ' . $response->getStatus() . ' ' .
    $response->getReasonPhrase();
  }
}
catch(HTTP_Request2_Exception $e) {
  echo 'Error: ' . $e->getMessage();
}
```
{% endcode %}
{% endtab %}

{% tab title="Java" %}
{% code title="Java - OkHttp" overflow="wrap" lineNumbers="true" %}
```java
OkHttpClient client = new OkHttpClient().newBuilder()
  .build();
MediaType mediaType = MediaType.parse("application/json");
RequestBody body = RequestBody.create(mediaType, "{\r\n    \"financedAmount\": 119.9,\r\n    \"solutionCode\": \"SCFRSP-4XTS\",\r\n    \"merchantBasketId\": \"647aeb24-a89c-11ed-afa1-0242ac120002\",\r\n    \"merchantGlobalOrderId\": \"XbB6_sMPbkvRk0y#206578\",\r\n    \"merchantBuyerId\": \"701943\",\r\n    \"merchantUrls\": {\r\n        \"confirmation\": \"https://mymerchand.domain/uri\"\r\n    },\r\n    \"buyers\": [\r\n        {\r\n            \"billingContact\": {\r\n                \"lastName\": \"Dupont\",\r\n                \"firstName\": \"Paul\",\r\n                \"commonTitle\": \"Mr.\",\r\n                \"email\": \"paul.dupont@mail.com\",\r\n                \"mobilePhoneNumber\": \"+33684749393\",\r\n                \"professionalTitle\": \"Professor\",\r\n                \"phoneNumber\": \"+33184749393\"\r\n            },\r\n            \"billingAddress\": {\r\n                \"locationType\": \"billingAddress\",\r\n                \"streetNumber\": 147,\r\n                \"streetNumberSuffix\": \"B\",\r\n                \"streetName\": \"main street\",\r\n                \"streetNameComplement\": \"block 47\",\r\n                \"zipCode\": \"92060\",\r\n                \"cityName\": \"Paris\",\r\n                \"regionName\": \"Île-de-France\",\r\n                \"countryCode\": \"FR\"\r\n            },\r\n            \"deliveryContact\": {\r\n                \"lastName\": \"Dupont\",\r\n                \"firstName\": \"Paul\",\r\n                \"commonTitle\": \"Mr.\",\r\n                \"email\": \"paul.dupont@mail.com\",\r\n                \"mobilePhoneNumber\": \"+33684749393\",\r\n                \"professionalTitle\": \"Professor\",\r\n                \"phoneNumber\": \"+33184749393\"\r\n            },\r\n            \"deliveryAddress\": {\r\n                \"locationType\": \"billingAddress\",\r\n                \"streetNumber\": 147,\r\n                \"streetNumberSuffix\": \"B\",\r\n                \"streetName\": \"main street\",\r\n                \"streetNameComplement\": \"block 47\",\r\n                \"zipCode\": \"92060\",\r\n                \"cityName\": \"Paris\",\r\n                \"regionName\": \"Île-de-France\",\r\n                \"countryCode\": \"FR\"\r\n            },\r\n            \"contact\": {\r\n                \"lastName\": \"Dupont\",\r\n                \"firstName\": \"P\",\r\n                \"commonTitle\": \"Mr.\",\r\n                \"email\": \"paul.dupont@mail.com\",\r\n                \"mobilePhoneNumber\": \"+33684749393\",\r\n                \"professionalTitle\": \"Professor\",\r\n                \"phoneNumber\": \"+33184749393\"\r\n            },\r\n            \"contactAddress\": {\r\n                \"locationType\": \"billingAddress\",\r\n                \"streetNumber\": 147,\r\n                \"streetNumberSuffix\": \"B\",\r\n                \"streetName\": \"main street\",\r\n                \"streetNameComplement\": \"block 47\",\r\n                \"zipCode\": \"92060\",\r\n                \"cityName\": \"Paris\",\r\n                \"regionName\": \"Île-de-France\",\r\n                \"countryCode\": \"FR\"\r\n            },\r\n            \"deliveryMethod\": \"Click & Collect\",\r\n            \"birthName\": \"Dupont\",\r\n            \"birthDate\": \"01021975\",\r\n            \"birthCityName\": \"Montpellier\",\r\n            \"birthCountryName\": \"FR\",\r\n            \"vip\": false\r\n        }\r\n    ],\r\n    \"basketDetails\": {\r\n        \"basketItems\": [\r\n            {\r\n                \"id\": \"M12345785513211\",\r\n                \"quantity\": 2,\r\n                \"model\": \"5KPM5\",\r\n                \"label\": \"PANTALON B MAGO\",\r\n                \"price\": 9500,\r\n                \"currencyCode\": \"EUR\",\r\n                \"orderId\": \"OD456742\",\r\n                \"brandName\": \"KitchenAid\",\r\n                \"description\": \"Le robot pâtissier à bol relevable très résistant idéal pour mixer de grandes quantités d'ingrédients, équipé d'un bol en acier inoxydable amovible.\",\r\n                \"specifications\": \"Puissance (W) 315, Tension (V) 220-240, Fréquence (Hz) 50/60\",\r\n                \"category\": \"R78757857\",\r\n                \"isFinanced\": true,\r\n                \"sku\": \"50\"\r\n            }\r\n        ]\r\n    }\r\n}");
Request request = new Request.Builder()
  .url("https://api.e-commerce.uatc.societegenerale.com/baas/uatc/e-financing/api/v1/subscriptions")
  .method("POST", body)
  .addHeader("Content-Type", "application/json")
  .addHeader("Authorization", "Bearer eyJlbmMiOiJBMjU2Q0JDLU...vTxWr8u9ooNMZ3zI")
  .build();
Response response = client.newCall(request).execute();
```
{% endcode %}
{% endtab %}

{% tab title="Python" %}
{% code title="Python Request" overflow="wrap" lineNumbers="true" %}
```python
import requests
import json

url = "https://api.scalexpert.uatc.societegenerale.com/baas/uatc/e-financing/api/v1/subscriptions"

payload = json.dumps({
  "financedAmount": 3000,
  "solutionCode": "SCFRSP-4XTS",
  "merchantBasketId": "647aeb24-a89c-11ed-afa1-0242ac120002",
  "merchantGlobalOrderId": "6Vh_mhvCUw9Nuvo#562850",
  "merchantBuyerId": "701943",
  "merchantUrls": {
    "confirmation": "https://mymerchand.domain/uri"
  },
  "buyers": [
    {
      "billingContact": {
        "lastName": "Dupont",
        "firstName": "Paul",
        "commonTitle": "MR",
        "email": "paul.dupont@mail.com",
        "mobilePhoneNumber": "+33684749393",
        "professionalTitle": "Professor",
        "phoneNumber": "+33184749393"
      },
      "billingAddress": {
        "locationType": "BILLING_ADDRESS",
        "streetNumber": 147,
        "streetNumberSuffix": "B",
        "streetName": "main street",
        "streetNameComplement": "block 47",
        "zipCode": "92060",
        "cityName": "Paris",
        "regionName": "Île-de-France",
        "countryCode": "FR"
      },
      "deliveryContact": {
        "lastName": "Dupont",
        "firstName": "Paul",
        "commonTitle": "MR",
        "email": "paul.dupont@mail.com",
        "mobilePhoneNumber": "+33684749393",
        "professionalTitle": "Professor",
        "phoneNumber": "+33184749393"
      },
      "deliveryAddress": {
        "locationType": "DELIVERY_ADDRESS",
        "streetNumber": 147,
        "streetNumberSuffix": "B",
        "streetName": "main street",
        "streetNameComplement": "block 47",
        "zipCode": "92060",
        "cityName": "Paris",
        "regionName": "Île-de-France",
        "countryCode": "FR"
      },
      "contact": {
        "lastName": "Dupont",
        "firstName": "Paul",
        "commonTitle": "MR",
        "email": "paul.dupont@mail.com",
        "mobilePhoneNumber": "+33684749393",
        "professionalTitle": "Professor",
        "phoneNumber": "+33184749393"
      },
      "contactAddress": {
        "locationType": "MAIN_ADDRESS",
        "streetNumber": 147,
        "streetNumberSuffix": "B",
        "streetName": "main street",
        "streetNameComplement": "block 47",
        "zipCode": "92060",
        "cityName": "Paris",
        "regionName": "Île-de-France",
        "countryCode": "FR"
      },
      "deliveryMethod": "Click & Collect",
      "birthName": "Dupont",
      "birthDate": "1990-10-21",
      "birthCityName": "Montpellier",
      "birthCountryName": "FR",
      "vip": False
    }
  ],
  "basketDetails": {
    "basketItems": [
      {
        "id": "M12345785513211",
        "quantity": 2,
        "model": "5KPM5",
        "label": "PANTALON B MAGO",
        "price": 1500,
        "currencyCode": "EUR",
        "orderId": "OD456742",
        "brandName": "KitchenAid",
        "description": "Le robot pâtissier à bol relevable très résistant idéal pour mixer de grandes quantités d'ingrédients, équipé d'un bol en acier inoxydable amovible.",
        "specifications": "Puissance (W) 315, Tension (V) 220-240, Fréquence (Hz) 50/60",
        "category": "R78757857",
        "isFinanced": True,
        "sku": "50"
      },
      {
        "id": "M12345786661",
        "quantity": 2,
        "model": "5KPM5",
        "label": "P",
        "price": 1500,
        "currencyCode": "EUR",
        "orderId": "OD456743",
        "brandName": "KitchenAid",
        "description": "Le robot pâtissier à bol relevable très résistant idéal pour mixer de grandes quantités d'ingrédients, équipé d'un bol en acier inoxydable amovible.",
        "specifications": "Puissance (W) 315, Tension (V) 220-240, Fréquence (Hz) 50/60",
        "category": "R78757887",
        "isFinanced": True,
        "sku": "ABC70"
      }
    ]
  }
})
headers = {
  'Content-Type': 'application/json',
  'Authorization': 'Bearer eyJlbmMiOiJBMjU2Q0JDL...aK9ljGv7cM8'
}

response = requests.request("POST", url, headers=headers, data=payload)

print(response.text)

```
{% endcode %}
{% endtab %}
{% endtabs %}

#### Step 4: Retrieve E-Financing Subscription Details

To retrieve the details of a specific e-financing subscription, follow these steps:

1. Get Subscription ID: Obtain the unique subscription ID associated with the e-financing subscription you want to retrieve details for.
2. Make a GET Request: Use the appropriate API endpoint, providing the unique subscription ID, to retrieve the subscription details.
3. Handle Response: Capture and process the response, which will contain comprehensive information about the requested subscription, including payment schedule, repayment amounts, and status.

{% tabs %}
{% tab title="Node.js" %}
{% code title="Node.Js - Native" overflow="wrap" lineNumbers="true" %}
```n4js
var https = require('follow-redirects').https;
var fs = require('fs');

var options = {
  'method': 'GET',
  'hostname': 'api.e-commerce.hml.societegenerale.com',
  'path': '/baas/uat/e-financing/api/v1/subscriptions/eb6adb12-5c1d-4b30-9b24-7854d755cd55',
  'headers': {
    'Authorization': 'Bearer eyJlbmMiOiJBMjU2Q0JDLUhTNTE...Uj6m2ZXbgRPYXZ_8wKIRfI'
  },
  'maxRedirects': 20
};

var req = https.request(options, function (res) {
  var chunks = [];

  res.on("data", function (chunk) {
    chunks.push(chunk);
  });

  res.on("end", function (chunk) {
    var body = Buffer.concat(chunks);
    console.log(body.toString());
  });

  res.on("error", function (error) {
    console.error(error);
  });
});

req.end();
```
{% endcode %}
{% endtab %}

{% tab title="PHP" %}
{% code title="PHP - HttpRequest2" overflow="wrap" lineNumbers="true" %}
```php
<?php
require_once 'HTTP/Request2.php';
$request = new HTTP_Request2();
$request->setUrl('https://api.e-commerce.hml.societegenerale.com/baas/uat/e-financing/api/v1/subscriptions/eb6adb12-5c1d-4b30-9b24-7854d755cd55');
$request->setMethod(HTTP_Request2::METHOD_GET);
$request->setConfig(array(
  'follow_redirects' => TRUE
));
$request->setHeader(array(
  'Authorization' => 'Bearer eyJlbmMiOiJBMjU2Q0...Uj6m2ZXbgRPYXZ_8wKIRfI'
));
try {
  $response = $request->send();
  if ($response->getStatus() == 200) {
    echo $response->getBody();
  }
  else {
    echo 'Unexpected HTTP status: ' . $response->getStatus() . ' ' .
    $response->getReasonPhrase();
  }
}
catch(HTTP_Request2_Exception $e) {
  echo 'Error: ' . $e->getMessage();
}
```
{% endcode %}
{% endtab %}

{% tab title="Java" %}
{% code title="Java - OkHttp" overflow="wrap" lineNumbers="true" %}
```java
OkHttpClient client = new OkHttpClient().newBuilder()
  .build();
MediaType mediaType = MediaType.parse("text/plain");
RequestBody body = RequestBody.create(mediaType, "");
Request request = new Request.Builder()
  .url("https://api.e-commerce.hml.societegenerale.com/baas/uat/e-financing/api/v1/subscriptions/eb6adb12-5c1d-4b30-9b24-7854d755cd55")
  .method("GET", body)
  .addHeader("Authorization", "Bearer eyJlbmMiOiJBMjU2Q0JDLUhTNTE...zR3VcUj6m2ZXbgRPYXZ_8wKIRfI")
  .build();
Response response = client.newCall(request).execute();
```
{% endcode %}
{% endtab %}

{% tab title="Python" %}
{% code title="Python Requests" overflow="wrap" lineNumbers="true" %}
```python
import requests

url = "https://api.scalexpert.uatc.societegenerale.com/baas/uatc/e-financing/api/v1/subscriptions/cd89186e-1054-4ed2-a4ce-e495082c689a"

payload = {}
headers = {
  'Authorization': 'Bearer eyJlbmMiOiJBMjU2Q0JDLU...ok-aK9ljGv7cM8'
}

response = requests.request("GET", url, headers=headers, data=payload)

print(response.text)
```
{% endcode %}
{% endtab %}
{% endtabs %}

Congratulations! :tada: You've now completed the API integration guide.&#x20;

Happy integrating! :clap:
