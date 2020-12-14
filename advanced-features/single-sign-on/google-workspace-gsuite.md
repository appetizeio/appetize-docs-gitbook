# Google Workspace \(GSuite\)

Several of our customers use Google Workspace \(GSuite\) as their SSO provider. Appetize.io support Google Workspace as an SSO provider, using the SAML protocol. 

For setup instructions, we recommend clients first follow our SAML instructions here:

{% page-ref page="saml.md" %}

Once basic SAML integration has been set up, there are a few additional steps required in order for a user's assigned roles to be contained in the SAML response from your server. 

### SSO configuration in Google Workspace

![ACS URL and Start URL will be provided by Appetize.io](../../.gitbook/assets/google_workspace_appetize_sso_configuration_1.png)

### Configure a new Role on the user object

![Define the Appetize\_role \(or name it as you wish\)](../../.gitbook/assets/google_workspace_appetize_sso_configuration_2.png)

### Map the newly defined role to the App attribute "groups"

![Map user role to &quot;groups&quot; attribute](../../.gitbook/assets/google_workspace_appetize_sso_configuration_3.png)

