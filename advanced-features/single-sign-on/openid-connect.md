# OpenID Connect

## **Overview**

The OKTA integration uses OAuth2 for authorization, and OpenID Connect \(OIDC\) for authentication \(admin vs. developer vs. non-admin roles\). 

### **Users and Roles:**

All user access and roles can be managed by OKTA. Within OKTA, you can configure which groups of users have access to the Appetize.io app. Please create a new group within OKTA, "appetize\_admin", which can be assigned to any admin users. Please also create a new group "appetize\_developer" , which can be assigned to any developer users.

NOTE: If mapping groups from Active Directory, they may appear as Okta-Appetize\_Admins and Okta-Appetize\_Developers, which are also supported. 

**OKTA App Setup:**

Please create a new Application within OKTA, type is "Web". 

![](file:////Users/jcsnyder/Library/Group%20Containers/UBF8T346G9.Office/TemporaryItems/msohtmlclip/clip_image001.png)

NOTE: There is a OKTA bug on the next screen where you set initial settings. If so, please click Done with default settings, then go back and edit afterwards. 

The settings for the app should match the following:

![](file:////Users/jcsnyder/Library/Group%20Containers/UBF8T346G9.Office/TemporaryItems/msohtmlclip/clip_image002.png)

Finally, we will need to configure OKTA to send over the user's groups with prefix appetize\_ after successful login. This can be done by adding the groups claim to your authorization server at API -&gt; Authorization Servers. 

![](file:////Users/jcsnyder/Library/Group%20Containers/UBF8T346G9.Office/TemporaryItems/msohtmlclip/clip_image003.png)

For some OKTA clients, this can also be done under the "Sign On" section in your app's configuration, where you can add groups the same way. 

**OKTA Settings for Appetize.io:**

1. We will need the "Client ID" and "Client secret" for the app you just created. 

![](file:////Users/jcsnyder/Library/Group%20Containers/UBF8T346G9.Office/TemporaryItems/msohtmlclip/clip_image004.png)

2. We will need the endpoint URLs for your OKTA authorization servers, including:

authorization\_endpoint

token\_endpoint

userinfo\_endpoint

jwks\_uri

issuer

introspection\_endpoint. 

These can be specified manually, but OKTA also provides a metadata endpoint \("Discovery URL"\) for convenience. For example, [https://dev-548472.oktapreview.com/oauth2/default/.well-known/oauth-authorization-server](https://dev-548472.oktapreview.com/oauth2/default/.well-known/oauth-authorization-server). 

Please let us know if any questions. We are also happy to assist setup via screen share if helpful.

