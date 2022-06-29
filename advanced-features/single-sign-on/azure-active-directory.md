# Azure Active Directory

Appetize.io supports Azure Active Directory as an SSO provider, using the SAML protocol.&#x20;

### Prerequisites

Please have the entity ID (usually `appetizeio-saml`) and the Assertion Consumer Service URL (looks like `https://appetize.io/sso/example/cb`) you received from Appetize support.

### Azure Active Directory Setup

In Azure Active Directory, go to Enterprise Applications. Create a new application. Choose a name for it (e.g. Appetize) and select "Integrate any other application you don't find in the gallery (Non-gallery).

![List of enterprise apps. Click "New Application"](../../.gitbook/assets/azure-1-enterprise-apps.png)

![Choose a name, e.g. "Appetize" and choose Non-gallery](../../.gitbook/assets/azure-2-create-app.png)

With the App created, click on "App roles". Create a role named "Appetize Admin" with value `appetize_admin`, and another role named "Appetize Developer" with value `appetize_developer`.

![Creating the appetizeadmin app role. Repeat for appetize\_developer.](../../.gitbook/assets/azure-3-create-app-role.png)

![Your app roles should look like this](../../.gitbook/assets/azure-4-app-roles.png)

Return to "Enterprise Applications" and choose "Appetize". Click "Users and groups" to authorize logging in. Click "Add user/group" and choose from your organization's existing users or groups. Select a role (Appetize Admin, Developer, or User) as appropriate. Save the assignment.

![Go to Users and Groups for the Appetize application](../../.gitbook/assets/azure-5-users-groups.png)

![Choose users and/or groups and assign them to the Admin, Developer, or User role](../../.gitbook/assets/azure-6-assign-user.png)

Click "Single sign-on" and click "SAML". Enter the entity ID and Assertion Consumer Service URL provided by Appetize support.

![Click SAML](../../.gitbook/assets/azure-7-sso.png)

![Enter values provided by Appetize support](../../.gitbook/assets/azure-8-saml-start.png)

On the next page, click the edit button next to "Attributes & Claims". Click "Add a new claim". Name: groups, Source: attribute, Source attribute: user.assignedroles. Save the claim.

![Click Edit button next to Attributes & Claims](../../.gitbook/assets/azure-9-saml-page.png)

![Click "Add new claim"](../../.gitbook/assets/azure-11-claims.png)

![Name: groups. Source attribute: user.assignedroles](../../.gitbook/assets/azure-12-new-claim.png)

Return the SAML page and download the "Federation Metadata XML" file. Send this file to Appetize support. Alternative, you may send the Certificate (Base64) and the Login URL.

![Download the Federation Metadata XML and send to Appetize support](../../.gitbook/assets/azure-13-saml-certificate.png)

Appetize will provision SSO for your account after receiving the information. If necessary, we may also schedule a call to test the integration.
