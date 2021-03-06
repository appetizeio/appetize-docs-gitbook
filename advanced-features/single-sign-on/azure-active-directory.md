# Azure Active Directory

Several of our customers use Azure Active Directory as their SSO provider. Appetize.io support Azure Active Directory as an SSO provider, using the SAML protocol. 

For setup instructions, we recommend clients first follow our SAML instructions here:

{% page-ref page="saml.md" %}

Once basic SAML integration has been set up, there are a few additional steps required in order for a user's assigned roles to be contained in the SAML response from your server. 

### Create the required roles

![App roles used by Appetize.io](../../.gitbook/assets/screen-shot-2020-12-04-at-9.48.35-am.png)

### Configure SAML to pass the user's assigned roles as a "groups" claim

![Configure SAML to include a user&apos;s assigned roles as a &quot;groups&quot; field in the SAML response](../../.gitbook/assets/screen-shot-2020-12-04-at-9.47.03-am.png)

