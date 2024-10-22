# Single Sign-On

{% hint style="info" %}
Single Sign-on is only available on our Enterprise plans. [Contact us](https://appetize.io/contact-us) to learn more.
{% endhint %}

Appetize supports SSO integrations using several different providers.

We have provided instructions below. We are also happy to setup and test the SSO integration over a phone call. In that case, please [contact us](mailto:hello@appetize.io).

{% hint style="warning" %}
Once SSO is enabled for your account, all user access and role assignments are managed entirely by your SSO provider.
{% endhint %}

### Role assignments

Please create the following groups within your SSO provider. Assigning users to each group is equivalent to granting them the corresponding role within your Appetize account.

{% hint style="info" %}
Appetize supports role names that matches the following regex:

`/(^|[-])appetize[-]{role}?$/i`
{% endhint %}

| Role                | Permissions                                                               |
| ------------------- | ------------------------------------------------------------------------- |
| appetize\_user      | Can only run uploaded apps.                                               |
| appetize\_developer | Can upload apps, delete apps, manage app settings.                        |
| appetize\_admin     | Can manage account settings, download usage reports, download audit logs. |

### Providers

{% content-ref url="openid-connect.md" %}
[openid-connect.md](openid-connect.md)
{% endcontent-ref %}

{% content-ref url="saml.md" %}
[saml.md](saml.md)
{% endcontent-ref %}

{% content-ref url="azure-active-directory.md" %}
[azure-active-directory.md](azure-active-directory.md)
{% endcontent-ref %}

{% content-ref url="google-workspace-gsuite.md" %}
[google-workspace-gsuite.md](google-workspace-gsuite.md)
{% endcontent-ref %}
