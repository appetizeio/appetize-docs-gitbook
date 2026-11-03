---
description: >-
  Seamlessly integrate Appetize into your CI/CD pipeline by making use of our
  REST API.
icon: cloud
---

# REST API

## 🚀 Getting Started

{% hint style="success" %}
**Private Instance Users**\
If you're using a **Private Enterprise Instance**, update the domain for your requests:

* For **v1 APIs**, use: `https://custom.appetize.io`
* For **v2 APIs**, use: `https://custom.appetize.io/api/`
{% endhint %}

### 1. Get Your API Token

Log in to the Appetize dashboard and navigate to [**Organization → API Token**](https://appetize.io/organization/api-token)

For full instructions on how to generate, manage and revoke tokens, see the [API Tokens guide](../account/api-tokens.md).

{% hint style="info" %}
You must be an organization admin to create or view tokens.
{% endhint %}

### 2.  Authenticate Your Requests

Use the `X-API-KEY` header to authenticate every API request.

{% tabs %}
{% tab title="cURL" %}
```bash
curl -X GET https://api.appetize.io/v1/apps \
  -H "X-API-KEY: your_api_token"
```
{% endtab %}

{% tab title="JavaScript " %}
```typescript
fetch("https://api.appetize.io/v1/apps", {
  headers: {
    "X-API-KEY": "your_api_token"
  }
})
.then(response => response.json())
.then(data => console.log(data))
.catch(error => console.error(error));
```
{% endtab %}
{% endtabs %}

### 3. Explore our API

You’re all set to start using the API.

Each endpoint includes:

* 📦 Sample requests and responses
* 🌐 Code samples in multiple languages (like cURL, Python, JavaScript)

Use these to quickly understand how each endpoint works and integrate it into your own tools.

## Format & Conventions

* **POST** requests must include a `Content-Type: application/json` header.
* All responses are in **JSON** format.

## Response Codes

| Status code            | Details                                               |
| ---------------------- | ----------------------------------------------------- |
| **200**                | OK - Everything worked as expected.                   |
| **400**                | Bad Request - Often missing a required parameter.     |
| **401**                | Unauthorized - No valid API token provided.           |
| **404**                | Not Found - No app found for **publicKey** specified. |
| **500, 502, 503, 504** | Server error - something went wrong on our server.    |
