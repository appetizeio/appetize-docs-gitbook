---
description: >-
  Enhance user satisfaction with automated sign-in using Appetize! Automate the
  process to save time and reduce friction.
---

# Automate Sign-in Flow

## Overview

Automating the sign-in flow refers to the process of enabling your mobile application to perform the sign-in or authentication process automatically, without requiring manual intervention from the user. Instead of users having to enter their credentials (e.g., username and password) each time they access the app, automation allows the app to handle this process programmatically.

There are a lot of use cases where this could be invaluable e.g. for call center agents, reducing the time to access the right screen can boost productivity and improve customer service.

There are various ways to achieve sign-in automation, but in this document we will focus on our two recommended approaches:

1. [**Launch Parameters**](automate-sign-in-flow.md#option-1-launch-parameters)
2. [**AppRecorder (UI Automation)**](automate-sign-in-flow.md#option-2-apprecorder-ui-automation)

### Option 1: Launch Parameters

With launch parameters, developers can pass authentication information as part of the app's URL or via our JavaScript SDK when opening it. The app then extracts the provided credentials and automatically signs the user in.

| Pros                               | Cons                             |
| ---------------------------------- | -------------------------------- |
| Most seamless experience for users | Requires mobile development work |

#### Preparing your Application:

* Make use of [Launch Params](../features/launch-params.md) to pass user credentials (e.g. username/password or authentication token) to your Application.

{% code title="Example of passing in Username and password" fullWidth="false" %}
```json
&params={"username":"{the user name}","password":"{the user password}"}
```
{% endcode %}

{% tabs %}
{% tab title="Android (Kotlin)" %}
The data will be passed as extras into the intent that launches your app e.g.&#x20;

```kotlin
val username = intent.getStringExtra("username")
val password = intent.getStringExtra("password")
// Start your authentication flow as usual
signInUser(username: username, password: password)
```
{% endtab %}

{% tab title="iOS (Swift)" %}
The data passed will be stored in the shared defaults object e.g.

```swift
let username = UserDefaults.standard.string(forKey: "username")
let password = UserDefaults.standard.string(forKey: "password")
// Start your authentication flow as usual
signInUser(username: username, password: password)
```
{% endtab %}
{% endtabs %}

* Make use of [Deep Links](../features/deep-links.md) to automatically navigate to the appropriate screen to reduce the time to load e.g. if your app has a welcome screen or an onboarding flow, you could skip that by launching directly into the login screen e.g.

```url
https://appetize.io/app/{public_key}?launchUrl=yourapp://signin
```

#### Some Additional Considerations:

Determine how you will pass the credentials to the Appetize client and session:

* [x] Credentials via Input Fields
* [x] Credentials via Query Parameters
* [x] Persisting credentials when the Launch Page (page that embeds the Appetize iframe) reloads

### Option 2: AppRecorder (UI Automation)

Using our UI automation functionality, developers can _script_ the steps a user takes during the sign-in process. These steps are then replayed automatically whenever the app is launched, mimicking the user's interactions to achieve sign-in.

| Pros                                                                                                                                                                                                                                                                             | Cons                                                                 |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------- |
| No development work required to imitate user behavior.                                                                                                                                                                                                                           | Generally slightly slower and less streamlined compared to Option 1. |
| Can also be used in conjunction with our other features such as [Deep Links](../features/deep-links.md) or [Launch Params](../features/launch-params.md) to get an even more streamlined experience (especially useful if the apps already have existing support for deep links) |                                                                      |

{% hint style="info" %}
For the best stability and to to facilitate the auto sign-in process, ensure your mobile application has all the necessary accessibility identifiers or resource identifiers set for the sign-in elements, such as the username input field, password input field, and sign-in button.
{% endhint %}

* Set up your Launch with our [JavaScript SDK](../javascript-sdk/getting-started.md).
* Determine how to retrieve the credentials e.g. via inputs on your Launch Page e.g.

```html
<label for="username" class="form-label">Username</label>
<input type="text" class="form-control" id="username" name="username" tabindex="1">
<label for="password" class="form-label">Password</label>
<input type="password" class="form-control" id="password" name="password" tabindex="2">
<a id="start_session" type="submit" tabindex="3">Start New Session</a>
```

```typescript
const startSessionButton = document.getElementById('start_session');
const usernameField = document.getElementById('username');
const passwordField = document.getElementById('password');
```

* If you have a custom button to start the session, add a function to start the Appetize session

```typescript
startSessionButton.addEventListener('click', async function(event) {
    if(!window.client) { return; }
    try {
        await window.client.startSession();
    } catch (error) {
        console.error(error);
    }
});
```

* Observe any **session** change events to invoke the automated steps to authenticate the user

```typescript
client.on("session", async session => {
    console.log('session started!')
    try {
         // Get username and password values
        var username = usernameField.value;
        var password = passwordField.value;
        await login(session, username, password);
    } catch (error) {
        console.error(error);
    }
});
```

* Run the automated steps to authenticate the user with the credentials that was provided. See [Touch Interactions](../javascript-sdk/automation/touch-interactions.md) for more samples on how to interact with the session:

{% hint style="warning" %}
These automated steps are just an example and need to be adjusted to match your actual application
{% endhint %}

```typescript
async function login(session, username, password) {
    // type username
     await session.tap({
        element: {
            attributes: {
                // android example
                'resource-id': 'username_field'
            }
        }
    });
    await session.type(username)
    
    // type password
    await session.tap({
        element: {
            attributes: {
                // iOS example
                accessibilityIdentifier: 'password_field'
            }
        }
    });
    await session.type(password)
    
    // tap login button
    await session.tap({ element: { text: 'Login' } })
}
```

{% hint style="info" %}
For a more complete example on how to automate the sign-in flow with our JavaScript SDK, see our [Pass Credentials Launch Page](https://github.com/appetizeio/appetize-samples/tree/main/pass\_credentials\_launch\_page) in our [Sample Repository](https://samples.appetize.io/).
{% endhint %}
