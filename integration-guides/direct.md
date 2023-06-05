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

#### Step 1: Initiate an E-Financing Subscription

To initiate an e-financing subscription for a customer, follow these steps:

1. Collect Customer Information: Gather the required customer information, such as name, contact details, and billing address.
2. Make a POST Request: Use the appropriate API endpoint, passing the necessary customer information and subscription details.
3. Handle Response: Capture and process the response, which will contain the subscription ID and any additional information provided by the API.

#### Step 2: Retrieve E-Financing Subscription Details

To retrieve the details of a specific e-financing subscription, follow these steps:

1. Get Subscription ID: Obtain the unique subscription ID associated with the e-financing subscription you want to retrieve details for.
2. Make a GET Request: Use the appropriate API endpoint, providing the unique subscription ID, to retrieve the subscription details.
3. Handle Response: Capture and process the response, which will contain comprehensive information about the requested subscription, including payment schedule, repayment amounts, and status.

#### Step 3: Check Eligible E-Financing Solutions

To determine the eligible e-financing solutions available for a specific purchase, follow these steps:

1. Collect Purchase Information: Gather relevant purchase details, such as the total amount and any other required parameters.
2. Make a POST Request: Utilize the API endpoint responsible for checking eligibility, passing the necessary purchase information.
3. Handle Response: Capture and process the response, which will indicate the available e-financing solutions and their associated terms and conditions.

{% tabs %}
{% tab title="Node.js" %}


{% code title="Node.js native" overflow="wrap" lineNumbers="true" fullWidth="true" %}
```n4js
// var https = require('follow-redirects').https;
var fs = require('fs');

var options = {
  'method': 'GET',
  'hostname': 'api.e-commerce.hml.societegenerale.com',
  'path': '/baas/uat/e-financing/api/v1/eligible-solutions?financedAmount=500&buyerBillingCountry=FR',
  'headers': {
    'X-BAAS-THIRD-PARTY-ID': '72f814b4-d4a0-4e6b-8ae2-777b24f279ef'
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
// <?php
require_once 'HTTP/Request2.php';
$request = new HTTP_Request2();
$request->setUrl('https://api.e-commerce.hml.societegenerale.com/baas/uat/e-financing/api/v1/eligible-solutions?financedAmount=500&buyerBillingCountry=FR');
$request->setMethod(HTTP_Request2::METHOD_GET);
$request->setConfig(array(
  'follow_redirects' => TRUE
));
$request->setHeader(array(
  'X-BAAS-THIRD-PARTY-ID' => '72f814b4-d4a0-4e6b-8ae2-777b24f279ef'
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
  .addHeader("X-BAAS-THIRD-PARTY-ID", "72f814b4-d4a0-4e6b-8ae2-777b24f279ef")
  .build();
Response response = client.newCall(request).executeaaTP
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
