---
description: >-
  Seamlessly integrate Appetize into your CI/CD pipeline by making use of our
  REST API.
---

# Overview

## Getting Started&#x20;

{% hint style="warning" %}
If you are using an Enterprise Private Instance of Appetize, please replace all API calls from **api.appetize.io** to your custom domain, eg. **custom.appetize.io**.
{% endhint %}

All users with _admin_ or _developer_ roles may request an API token after logging in and navigating to your [Account Dashboard](https://appetize.io/account).

See our [Sample Code](sample-code.md) for an example on how to get started.

### HTTP Requests

{% hint style="info" %}
All HTTP POST Requests must use JSON.
{% endhint %}

### HTTP Responses

{% hint style="info" %}
All HTTP Responses will be in JSON.
{% endhint %}

| Status code                 | Details                                               |
| --------------------------- | ----------------------------------------------------- |
| <h4>200</h4>                | OK - Everything worked as expected.                   |
| <h4>400</h4>                | Bad Request - Often missing a required parameter.     |
| <h4>401</h4>                | Unauthorized - No valid API token provided.           |
| <h4>404</h4>                | Not Found - No app found for **publicKey** specified. |
| <h4>500, 502, 503, 504</h4> | Server error - something went wrong on our server.    |
