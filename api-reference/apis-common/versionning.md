---
description: Versioning overview
---

# Versioning

All APIs are versioned following the structure depicted below:

`V X.xx.xx` of which

* first digits represent the major version
* second digits represent the minor version
* and third digits represents patches changes&#x20;

The major version is also included in the path url ex: "`e-financing/api/v1`" meaning the endpoints and operations under this path are only referring this major version.&#x20;

Minor versions and patches change will not impact the url meaning the endpoints will always refers to the last minor and patches changes under the major version.

{% hint style="warning" %}
All change under major version are ascendant compatibles. In case of breaking that compatibility, a new major version will be created.
{% endhint %}

We will mention in the API reference pages of this guide the content of change operated in the versions and also we will keep the history of version change.

{% hint style="info" %}
In the developer portal we will reference only the last version of APIs. But we will make available last and previous major versions during a 6 months minimum  period to allow customers making migration under last version.
{% endhint %}

