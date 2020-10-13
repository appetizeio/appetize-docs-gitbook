# Single sign-on

Appetize.io supports SSO integrations using either OpenID Connect \(OIDC\) or SAML.

We have provided instructions below. We are also happy to setup and test the SSO integration over a phone call. In that case, please [contact us](mailto:hello@appetize.io).

Once SSO is enabled for your account, all user access and role assignments are managed entirely by your SSO provider. 

### Role assignments

Please create the following groups within your SSO provider. Assigning users to each group is equivalent to granting them the corresponding role within your Appetize.io account. 

| Role | Permissions |
| :--- | :--- |
| appetize\_user | Can only run uploaded apps. |
| appetize\_developer | Can upload apps, delete apps, manage app settings. |
| appetize\_admin | Can manage account settings, download usage reports, download audit logs. |



{% page-ref page="openid-connect.md" %}

{% page-ref page="saml.md" %}





