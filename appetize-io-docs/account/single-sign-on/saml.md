# SAML

{% hint style="info" %}
_Every SSO provider is a little bit different. Please_ [_contact us_](mailto:hello@appetize.io) _with any questions!_
{% endhint %}

## Configure app settings

Please ensure that the user's email address is sent as the username in the SAML response.

Please create group assignments for `appetize_developer` and `appetize_admin`, and assign to users appropriately. All users who have access to the SAML app, with no group assignments, will default to the user role. Please ensure these group assignments are passed in the SAML response as an attribute named `groups`.

| Field                                | Value                            |
| ------------------------------------ | -------------------------------- |
| SP Entity Id / Audience URI          | appetizeio-saml                  |
| Assertion Consumer Service URL (ACS) | TBD - provided by Appetize.io    |
| Recipient URL                        | N/A - leave blank or same as ACS |
| Destination URL                      | N/A - leave blank or same as ACS |

## **Information to provide to Appetize**

* **entryPoint** - the URL from your service provider that will initiate a login.
* **x509 certificate** used to sign SAML responses

{% hint style="info" %}
your provider may provide an **IdP metadata file** that contains both the **entryPoint** and the **x509 certificate**. You may send that file to us.
{% endhint %}

* authentication context (optional) - usually necessary for Microsoft ADFS
* **signature algorithm** (default SHA256)
* which **identify provider** are you using? (ADFS, OKTA, etc)

## Example Configuration with OKTA

<figure><img src="../../.gitbook/assets/screenshot-okta-saml-1-app.png" alt="Creating a SAML app"><figcaption><p>Creating a SAML app</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/screenshot-okta-saml-2-general.png" alt="General Settings - you may customize as you see fit"><figcaption><p>General Settings - you may customize as you see fit</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/screenshot-okta-saml-3-samlconfig.png" alt="Enter the Single Sign On URL Provided by Appetize"><figcaption><p>Enter the Single Sign On URL Provided by Appetize.</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/screenshot-okta-saml-4-idp-metadata.png" alt="Save the IdP metadata file and send to Appetize.io"><figcaption><p>Save the IdP metadata file and send to Appetize.io</p></figcaption></figure>
