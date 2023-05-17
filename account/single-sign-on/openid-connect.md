# OpenID Connect

{% hint style="info" %}
_Every SSO provider is a little bit different. Please_ [_contact us_](mailto:hello@appetize.io) _with any questions!_
{% endhint %}

## Create a new application

<figure><img src="../../.gitbook/assets/image (1) (1) (2).png" alt="Example creating new &#x22;Web&#x22; application in OKTA"><figcaption><p>Example creating new "Web" application in OKTA</p></figcaption></figure>

## Configure app settings

| Field               | Value                         |
| ------------------- | ----------------------------- |
| Allowed grant types | Authorization Code            |
| Login redirect URIs | TBD - provided by Appetize.io |
| Initiate login URI  | TBD - provided by Appetize.io |

<figure><img src="../../.gitbook/assets/image (5) (1) (1) (1).png" alt="Example app settings in OKTA"><figcaption><p>Example app settings in OKTA</p></figcaption></figure>

### Add group assignments to claims

We will need to configure your SSO provider to send over the user's groups assignments after a successful login.

The following example shows how to pass through groups with prefix appetize\_\* as a groups claim within OKTA. This can be done by adding the groups claim to your authorization server at API -> Authorization Servers. For some OKTA clients, this can also be done under the "Sign On" section in your app's configuration, where you can add groups the same way.

<figure><img src="../../.gitbook/assets/image (3) (2) (1) (1).png" alt="Example including appetize_* group assignments claim in OKTA"><figcaption><p>Example including appetize_* group assignments claim in OKTA</p></figcaption></figure>

## **Information to provide to Appetize**

1\. We will need the "**Client ID**" and "**Client secret**" for the app you just created.

<figure><img src="../../.gitbook/assets/image (6) (1).png" alt="Example Credentials to provide to Appetize.io"><figcaption><p>Credentials to provide to Appetize.io</p></figcaption></figure>

2\. We will also need your **metadata endpoint**, often called "Discovery URL". For example: [https://dev-548472.oktapreview.com/oauth2/default/.well-known/oauth-authorization-server](https://dev-548472.oktapreview.com/oauth2/default/.well-known/oauth-authorization-server)

If the metadata endpoint is not available, you may also specify the required fields below:

* **authorization\_endpoint**
* **token\_endpoint**
* **userinfo\_endpoint**
* **jwks\_uri**
* **issuer**
* **introspection\_endpoint**
