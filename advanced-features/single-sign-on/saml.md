# SAML

_Note: Every SSO provider is a little bit different. Please _[_contact us_](mailto:hello@appetize.io)_ with any questions!_

### Configure app settings

Please ensure that the user's email address is sent as the username in the SAML response. 

Please create group assignments for _appetize_developer_ and _appetize_admin_, and assign to users appropriately. All users who have access to the SAML app, with no group assignments, will default to _appetize_user_ role. Please ensure these group assignments are passed in the SAML response. 

| Field                                | Value                         |
| ------------------------------------ | ----------------------------- |
| SP Entity Id (audience id)           | appetizeio-saml               |
| Assertion Consumer Service URL (ACS) | TBD - provided by Appetize.io |
| Recipient URL                        | N/A - leave blank             |
| Destination URL                      | N/A - leave blank             |

### **Information to provide to Appetize.io**

* entryPoint
* issuer
* x509 cert used to sign SAML responses
* authnContext (if applicable)
* signature algorithm (default SHA256)
* which identify provider are you using? (ADFS, OKTA, etc)

