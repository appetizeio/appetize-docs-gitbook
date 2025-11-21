---
description: >-
  API Tokens allow your organization to authenticate automated workflows and
  access the Appetize REST API.
---

# API Tokens

You can manage your organization's API tokens by navigating to [**Organization → API Tokens**](https://appetize.io/organization/api-tokens)

{% hint style="warning" %}
Tokens belong to the organization, not to individual users.&#x20;

If a user who generated a token is removed from the organization, the token continues to work.
{% endhint %}

## Generating an API Token

Admins can create a new token by selecting **Generate API Token**.

You will be asked to provide:

* **Label**\
  A short name that identifies how this token will be used, such as a CI system, a script, or an internal tool. The label helps you recognize activity created by this token. We recommend not reusing the same label twice.
* **Role**\
  Choose the level of access the token should have.\
  Pick the least-privileged role that matches your automation’s needs.

Select **Generate Token** to create it.

<figure><img src="../.gitbook/assets/image (73).png" alt=""><figcaption></figcaption></figure>

After the token is created:

* The full token appears once. Copy and save it securely, because it cannot be viewed again.
* All organization admins will receive an email with the creator, the time it was generated, and an obfuscated version of the token.

<figure><img src="../.gitbook/assets/image (74).png" alt=""><figcaption></figcaption></figure>

## Viewing Tokens

<figure><img src="../.gitbook/assets/image (75).png" alt=""><figcaption></figcaption></figure>

Admins can view all API Tokens in the organization. Each token displays:

* **Label**\
  The name given when the token was created, useful for identifying where the token is used.
* **Token**\
  A partially masked version of the token, shown for reference only. The full token is never displayed again after creation.
* **Last used**\
  Indicates the most recent time the token authenticated a request.
* **Created by**\
  Shows who originally generated the token.&#x20;
* **Role**\
  Indicates whether the token was created with Developer or Admin privileges.
* **Delete icon**\
  Allows an admin to revoke the token.

## **Revoking Tokens**

To revoke a token, select the bin icon next to it.\
A confirmation dialog appears and you will be asked to type the token’s label to confirm the removal.

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

Once a token is revoked, any integrations using this token will lose its functionality immediately.
