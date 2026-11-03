---
description: >-
  Several of our customers use Google Workspace (GSuite) as their SSO provider.
  Appetize support Google Workspace as an SSO provider, using the SAML protocol.
---

# Google Workspace (GSuite)

For setup instructions, we recommend clients first follow our SAML instructions here:

{% content-ref url="saml.md" %}
[saml.md](saml.md)
{% endcontent-ref %}

Once basic SAML integration has been set up, there are a few additional steps required in order for a user's assigned roles to be contained in the SAML response from your server.

## SSO configuration in Google Workspace

<figure><img src="../../.gitbook/assets/google_workspace_appetize_sso_configuration_1.png" alt=""><figcaption><p>ACS URL and Start URL will be provided by Appetize.io</p></figcaption></figure>

## Configure a new Role on the user object

<figure><img src="../../.gitbook/assets/google_workspace_appetize_sso_configuration_2.png" alt=""><figcaption><p>Define the Appetize_role (or name it as you wish)</p></figcaption></figure>

## Map the newly defined role to the App attribute "groups"

<figure><img src="../../.gitbook/assets/google_workspace_appetize_sso_configuration_3.png" alt=""><figcaption><p>Map user role to "groups" attribute</p></figcaption></figure>
