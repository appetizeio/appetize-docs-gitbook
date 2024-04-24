---
description: >-
  Seamlessly integrate Appetize into your CI/CD pipeline by making use of our
  REST API.
---

# Overview

## Getting Started

{% hint style="warning" %}
If you are using an Enterprise Private Instance of Appetize, please replace all API calls from **api.appetize.io** to your custom domain, e.g. **custom.appetize.io**.
{% endhint %}

1. **Get Your API Token**\
   All users with _admin_ or _developer_ roles may request an API token after logging in and navigating to your [Account Dashboard](https://appetize.io/account).
2. **Use Basic Authentication:**\
   When sending requests to the Appetize REST API that requires authentication, use Basic Authentication.
3. **Encode your token** using Base64 encoding.&#x20;
4. **Attach Token to Requests**\
   In your HTTP headers, include an Authorization header with the value "Basic" followed by the encoded token.

See our [Sample Code](sample-code.md) for an example on how to get started.

### HTTP Requests

{% hint style="info" %}
All HTTP POST Requests must use JSON.
{% endhint %}

### HTTP Responses

{% hint style="info" %}
All HTTP Responses will be in JSON.
{% endhint %}

| Status code            | Details                                               |
| ---------------------- | ----------------------------------------------------- |
| **200**                | OK - Everything worked as expected.                   |
| **400**                | Bad Request - Often missing a required parameter.     |
| **401**                | Unauthorized - No valid API token provided.           |
| **404**                | Not Found - No app found for **publicKey** specified. |
| **500, 502, 503, 504** | Server error - something went wrong on our server.    |
