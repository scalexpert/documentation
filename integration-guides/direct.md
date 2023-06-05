---
description: How to integrate our solutions with APIs
---

# APIs

> DRAFT

## API Integration Guide (for E-Financing Solution - temp)

### Table of Contents

1. Introduction
2. API Overview
3. Getting Started
4. API Integration Steps
5. Best Practices and Considerations
6. Troubleshooting and Support

### 1. Introduction

This API integration guide will walk you through the process of setting up your environments so you can later consume SG's e-commerce APIs into your application or platform.

By integrating these APIs, you'll be able to initiate and manage e-financing subscriptions on behalf of your customers or dynamically propose warranty extensions for some items on their basket prior checkout.

### 2. API Overview

The APIs allows you to interact with the our platform programmatically, enabling you to initiate and manage financing or insurance proposals seamlessly. Here are some key aspects of the APIs:

* RESTful architecture: Utilize standard HTTP methods (GET, POST, PUT, DELETE) to interact with the API.
* JSON-based data format: Send and receive data in JSON format, ensuring compatibility and ease of integration across different programming languages.

#### Authentication and Authorization

To access these APIs, you'll need to authenticate your requests : API Keys are obtained from the developer portal, which serves as your access credential. They are used to authenticate your service using OAuth 2.0 client credentials workflow. Upon authorization for the claimed scopes the issued token will be used to identify each subsequent request.

To retrieve your API keys Refer to the **API key** page:

{% content-ref url="../developers-docs/before-you-start/api-key.md" %}
[api-key.md](../developers-docs/before-you-start/api-key.md)
{% endcontent-ref %}

Refer to documentation of **oAuth2 API** for detailed information on GET /token endpoint:

{% content-ref url="../api-reference/authorization-server-api.md" %}
[authorization-server-api.md](../api-reference/authorization-server-api.md)
{% endcontent-ref %}

`(basic steps overview)`

#### API Endpoints and Request/Response Formats

The API provides various endpoints for managing subscriptions or retrieving relevant data. Each endpoint supports specific actions and requires specific parameters. Requests should include appropriate headers, and responses are returned in JSON format.

Refer to the **API reference** section for detailed information on each endpoint, including request/response examples and required parameters.

`(link to subsection)`

### 3. Getting Started

#### Prerequisites for Integration

Before starting the integration process, make sure you have the following:

* Developer Account: Create an account on the developer portal to access the API documentation, obtain API keys, and manage your integration.
* Platform Compatibility: Ensure that your application meets the technical requirements&#x20;

`(TODO : add technical requirements/restrictions)`

#### API Access Credentials and Keys

`(step by step screenshots & samples)`

#### Testing Environment Setup

Set up a testing environment to ensure smooth integration and testing of the E-Financing API:

* Sandbox: test environment that will simulates the production environment. Use this environment for development, integration, and testing purposes.
* API Documentation and SDKs: Familiarize yourself with the API documentation, including endpoint details, request/response examples, and any available SDKs or client libraries that can expedite the integration process.`(add sample code in PHP and JS => most e-commerce solutions are php-based and lots of js backend developer are copy/paste gurus)`

### 4. API Integration Steps

Now let's dive into the steps involved in integrating the **E-Financing** API into your application or platform:

#### Step 1: Check Eligible E-Financing Solutions

To determine the eligible e-financing solutions available for a specific purchase, follow these steps:

1. Collect Purchase Information: Gather relevant purchase details, such as the total amount and any other required parameters.
2. Make a POST Request: Utilize the API endpoint responsible for checking eligibility, passing the necessary purchase information.
3. Handle Response: Capture and process the response, which will indicate the available e-financing solutions and their associated terms and conditions.

{% tabs %}
{% tab title="Node.js" %}


{% code title="Node.js native" overflow="wrap" lineNumbers="true" fullWidth="true" %}
```n4js
var https = require('follow-redirects').https;
var fs = require('fs');

var options = {
  'method': 'GET',
  'hostname': 'api.e-commerce.hml.societegenerale.com',
  'path': '/baas/uat/e-financing/api/v1/eligible-solutions?financedAmount=500&buyerBillingCountry=FR',
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
$request->setUrl('https://api.e-commerce.hml.societegenerale.com/baas/uat/e-financing/api/v1/eligible-solutions?financedAmount=500&buyerBillingCountry=FR');
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
  .url("https://api.e-commerce.hml.societegenerale.com/baas/uat/e-financing/api/v1/eligible-solutions?financedAmount=500&buyerBillingCountry=FR")
  .method("GET", body)
  .addHeader("Authorization", "Bearer eyJlbmMiOiJBMjU2Q0JDLUhTN...Wr8u9ooNMZ3zI")
  .build();
Response response = client.newCall(request).execute();
```
{% endcode %}
{% endtab %}
{% endtabs %}

#### Step 2: Initiate an E-Financing Subscription

To initiate an e-financing subscription for a customer, follow these steps:

1. Collect Customer Information: Gather the required customer information, such as name, contact details, and billing address.
2. Make a POST Request: Use the appropriate API endpoint, passing the necessary customer information and subscription details.
3. Handle Response: Capture and process the response, which will contain the subscription ID and any additional information provided by the API.

{% tabs %}
{% tab title="Node.js" %}
{% code title="Node.js - Native" overflow="wrap" lineNumbers="true" %}
```n4js
var https = require('follow-redirects').https;
var fs = require('fs');

var options = {
  'method': 'POST',
  'hostname': 'api.e-commerce.hml.societegenerale.com',
  'path': '/baas/uat/e-financing/api/v1/subscriptions',
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
$request->setUrl('https://api.e-commerce.hml.societegenerale.com/baas/uat/e-financing/api/v1/subscriptions');
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
  .url("https://api.e-commerce.hml.societegenerale.com/baas/uat/e-financing/api/v1/subscriptions")
  .method("POST", body)
  .addHeader("Content-Type", "application/json")
  .addHeader("Authorization", "Bearer eyJlbmMiOiJBMjU2Q0JDLU...vTxWr8u9ooNMZ3zI")
  .build();
Response response = client.newCall(request).execute();
```
{% endcode %}
{% endtab %}
{% endtabs %}

#### Step 3: Retrieve E-Financing Subscription Details

To retrieve the details of a specific e-financing subscription, follow these steps:

1. Get Subscription ID: Obtain the unique subscription ID associated with the e-financing subscription you want to retrieve details for.
2. Make a GET Request: Use the appropriate API endpoint, providing the unique subscription ID, to retrieve the subscription details.
3. Handle Response: Capture and process the response, which will contain comprehensive information about the requested subscription, including payment schedule, repayment amounts, and status.

{% tabs %}
{% tab title="Node.Js" %}
{% code title="Node.Js - Native" overflow="wrap" lineNumbers="true" %}
```n4js
var https = require('follow-redirects').https;
var fs = require('fs');

var options = {
  'method': 'GET',
  'hostname': 'api.e-commerce.hml.societegenerale.com',
  'path': '/baas/uat/e-financing/api/v1/subscriptions/eb6adb12-5c1d-4b30-9b24-7854d755cd55',
  'headers': {
    'Authorization': 'Bearer eyJlbmMiOiJBMjU2Q0JDLUhTNTEyIiwiYWxnIjoiQTI1NktXIn0.06ALV6adjiwK274VbFC8XP3GQjDZaO-DOaIHUgmLkCNxO-nKXJFiVJ-OKykAR6RiMzDts6WCGiRWZs1cIvaAjOXTumNt0Pfj.pF3dwx836U1DiBYDX4CCHg.Wz9Zp_pHqaypsyNVJsYIPgTPJ0-1VM46dp1pSPIxRUa5Fdr-ZiSps59Lp9SE8sF5CY_DmYW-T_L6PL9dQZI1FGiSYDRNKJw4NoQhst81xYxzXlEsKSiwn3MLP2-Uy3Ca5IX6NOeIA45GG5DTrPSKGddmAbEsK1IBryivRpjKJoE2d_Psv-wvw1sEKhvRxcStSScUpxwUx5Y7OronbC7yQNIz9DeEy0asDj8TWh4a9MHM8hCwuS2Z49X-G0vsPp-KFzDfQ86XYuXQkrCsDyfiKaIZdKSOAv9FrqSBzSHISkrUEqLUqU6ijLZKJDp1IWakn4wX549kCupad-70PZ0K49Qr5aNm29x9CR09zJKdfqZ8_NR-wH-H5NCZB367vQdocC3nOTIVLbnAULNzqZ164gpg-Lwt2MnrayVMR3r9EWIijS1k79jPsqGNTv3_PDZV5FIqbWmYqXz5vWlII7ppH07FJWrOx9VDFZc6Zu8-HsGwz00zbySIgylqe2sSva_l2pcEsMmXkXc9Etwf7jIl2Ml--zkwvmRk2MeLlP0cZFaTdrGNw7FM1zE8oUHVeHxBOQ8f6XwBC8jdBSQ9WFq_PvKUhZFnKBPGGURPR2TAMfMoTFVcBqP30WTmXGdfciSo4asRPeuvnId0AVOky1OEmX-emg44ggLN7yniGWMGNfhvFMdKG-E6Xm3wsIeiJPAAekdUwfq2jRRF2fxxmznA01rucPpzz7e_7uApdgDXbOuuk8kV0pl1gNzE51Au-Mswo6YlweM5xMVleZaDY5oS8MAMSTmKl24yafJSvKl3Dg4xjNHA3XayEYbRHPXVrY6JpPV9SVk9kN9BgmSMMBF50iz4xT-fhF_avCEkxkWLvdyxPLZQqbUTIGWYCtOEIRNjea9lFp10ISNQbEBH2DqwMFYUbs0wDdmNrJBhIb-NTbGiTp9VyV68FYPOhIY722fUDbOwSV1uo43m3Nx65pj_wA-1tXsVDW18DFwwyxj8y8JN37i7Pro89e4a4zELXMvqFwE4-Fjx7Y7eT8t9rbyNUVEeis9VAExqYM8y1QWFBXBqSf2uM9x8crTqx_EHeqXZ3JrGqIuUpEO9ynLvvajwygl4MTJslTUsrRKf6LcR35kW2oH0oTjc1JKffil54UFf0Da37oukCg0g2CHsXnXIQsWN3CUNrh5_KF5jr0Nn4mEJfZGjsEDB0sYChT9wi_R3Ac8ABqHzQU8YcYIFabq6jAWxPgQXi3-I4X6C8or3y9vQ0HY-Wc9fJfawhPC3mkQtMgNBCSW-RNXlqfpWDqpyjFwskrsj7dZHCaAJn97yOFxSjA7jP4vP1c7BRl0bIgAJoqXMqHEkAaWu9Luzvjdg5YzGIypf4YtzCpFa69WXQpSV_f7vjjD_EP1Makjr5yF7051gQny9U_U_bvzVtXYekLlrfRBDdOmDbQauQqmFZQxLLxCfxftlR-5rc1-MyXC4LTicMQlKRk4coxbyMJAzQJYFPOigAAVmd5mP2r1btgb1TA2dJ6ujkiKyjeglhF5ebu-OPzVFl1BLyu7FUTd2-fzUi3rNcXEmPG_6m8pVvsKPgDYl0Ui_gyn5548TRE7-u0zOsjYdKpH5iHUQ8x__hoOBfE0iC55lYcRXD6baInSDVyyIgQP3kJO2x_EFLoJfzoHAbMXah7AyuZqM0ZeM_P90W3ooIkCwzXr62yWnPBXVsK1rdHR0spPuXxpkJwrKjUx4b5J9g5QkUi-sz0xRleXniSHXU3JOy5U_gID8f_TOLGsLf84dTrHJVOsOx9ydqa7nSwE2RA7q6t_EcT9FWwgOuEJVwSjaCRixgVcXO_M4ttI_OmK6rSGhZC_CkQDBgN11unNjV1A59Dq5mGV3nWzZSemdv3AUbEPnQn4ttAZqBf3tv80pEWXk8VHUh0jcCQy4AupiU5_68Rf3qdWwV-GC0z5eEiy4Jaggc-j7fOX2plDMDko76CuDmjJ_0S3TVO7xAE7D3HWuhOy3VMlo1rBVcwAMndY_ePHHSZIbiJ6AUqzfZ_wnaCKCrFHByZd2QudaCkdukTSuRGjI6lEwYeOesR4rYjwn0uUFTBRtwGOjyWijjeNTXyqUP3NS3KDapo2BCUgKT-tjPSN-pU_YwThAXf7akFoejHqGBCHWx89ns4rvEdZPy1L0z24orSe_aUXSXNzunPNhVxGOxW-iiK4ZuxqPBaVdVE8JfFp_0coFNM4KLu3AB0YvVU_OxIpUkRXoX9ifs_2RnmiFrFPutH49C5CiP0wQJPWgNGPdfFyS0bkYj8t0nD_KPUdf48yP8VBTxqbWBOpj3b-NrlSAnCqycU0EiE-NyStCE0pnIiPrZJea2_6jEj7_1an4bvuepITpDwR0VF61mEAJuMj-ZCPLtDrbz0TtTuONcDZSZbcyepaaU0T-Id5HF5rkM9Sq.7H_GoJj5kqCRj1J9zR3VcUj6m2ZXbgRPYXZ_8wKIRfI'
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
{% endtabs %}

### 5. Best Practices and Considerations

To ensure a successful API integration and optimal performance, consider the following best practices:

* Data Security and Privacy: Follow secure coding practices, encrypt sensitive data, and adhere to industry standards for data protection and privacy. \
  `(TODO : add content to security best practices page)`
* Error Handling and Error Codes: Implement robust error handling mechanisms to gracefully handle API errors and provide meaningful error messages to users. \
  `(TODO : add an error handling page)`
* Performance Optimization: Optimize API requests and responses for efficiency, minimize unnecessary data transfers, and utilize caching mechanisms where applicable. \
  `(TODO : provide guidance on effective token usage and renewal)`
* Versioning and API Updates: Stay up-to-date with the E-Financing provider's API updates and versioning practices, ensuring compatibility and avoiding disruptions during future updates. \
  `(TODO : add versioning rule page)`

### 6. Troubleshooting and Support

During the integration process, you may encounter issues or require assistance. Here are some resources for troubleshooting and support:

* Documentation and Developer Resources: Refer to the comprehensive API documentation, integration guides, and FAQs.\
  `(TODO : add FAQ section and feedback form/email for continuous improvement)`
* Support Channels: Reach out to the support team through designated channels, such as email, support tickets, or community forums, for assistance with specific integration issues.\
  `(TODO ??? create a public slack or equivalent with a bot who send an email to a support team when nobody is connected)`
* Integration Testing: Conduct thorough testing in your development environment to identify and resolve any integration-related issues before deploying to production.

Congratulations! You've now completed the API integration guide.&#x20;

Happy integrating!
