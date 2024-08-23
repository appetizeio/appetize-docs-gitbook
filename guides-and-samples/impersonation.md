---
description: >-
  Learn how to utilize Appetize for user impersonation and delegation scenarios,
  allowing call center agents or administrators to verify and troubleshoot
  user-reported issues.
---

# Impersonation

## Overview

Impersonation and delegation enable call center agents or system administrators to take on a user's identity to verify and troubleshoot user-reported issues. Most organizations already have a solution implemented for their web-based applications. Appetize allows you to impersonate and delegate your native and cross-platform mobile application users.

{% hint style="warning" %}
Enabling user impersonation necessitates the use of custom code and careful consideration of security, privacy, and compliance. The required custom code may involve making adjustments to the mobile app, the page Appetize is embedded on, and the backend infrastructure.
{% endhint %}

This documentation provides insights on leveraging Appetize's capabilities to impersonate users, perform delegated actions, and resolve user-reported problems. To simplify the process, we will break down impersonation into three essential steps:

* [Preparing User Context for Impersonation](impersonation.md#preparing-user-context-for-impersonation)
* [Passing the Impersonated User to your Embedded App](impersonation.md#passing-the-impersonated-user-to-your-embedded-app)
* [Best Practices](impersonation.md#best-practices)

## Preparing User Context for Impersonation

To begin the impersonation process, identify the target user's relevant information, such as identity, roles, and permissions that you would like to impersonate.

### **Token Generation Strategy**&#x20;

Understand how authentication works in your target app and use a strategy to generate a token based on the target user's context or specific scenarios. Some sample strategies could include:

* **Session-based Authentication**: Generate a JWT token based on the authenticated user's session.
* **OAuth2 Authentication**: Utilize the impersonation scope in OAuth2 to generate a token for specific users and behaviors.
* **OpenID Connect Authentication:** Update the token's subject (sub) claim and re-sign it to assume the identity of the desired user
* **Override Authentication:**  Implement a mechanism that allows admin users with elevated privileges to bypass the standard token validation process.

### **Option 1: Internal REST API and Web Interface (recommended)**

Use an internal REST API and web interface that allows administrators or call center agents to generate tokens with specific user roles and behaviors. The web interface can provide an intuitive interface for administrators to input the desired parameters, and the API can generate and return the corresponding token. This token can then be passed to the Appetize client via our [JavaScript SDK](broken-reference). See [Implementing Impersonation in Your App](impersonation.md#implementing-impersonation-in-your-app).

<img src="../.gitbook/assets/file.excalidraw (2).svg" alt="Sample Structure for using an internal API for generating the user token and passing it back to your embedded app." class="gitbook-drawing">

### **Option 2: Companion App**&#x20;

Use a companion app that works alongside the target app on Appetize. The companion app can include features to generate tokens with desired user roles and behaviors. The generated token can then be passed to the target app as a launch parameter or via deep link. See [Implementing Impersonation in Your App](impersonation.md#implementing-impersonation-in-your-app).

{% hint style="info" %}
You can run multiple embedded Appetize sessions and use our [JavaScript SDK](broken-reference) to pass the values between them or you could make use of our [App Groups](../platform/app-management/listing-apps.md#grouped-applications) to bundle the companion and the main app into a single session.
{% endhint %}

<img src="../.gitbook/assets/file.excalidraw (1) (1).svg" alt="Sample Structure for using a companion app for generating the user token and passing it back to your embedded app." class="gitbook-drawing">

### **Option 3: App Build for Appetize**

Use a dedicated/custom app build/flavor specifically for Appetize, that includes a token generation feature. This app can allow administrators or call center agents to input desired user roles and behaviors (or user id / email) and generate the corresponding token.&#x20;

{% hint style="info" %}
You could confirm that your app is running in an Appetize Session by making use of our default [Launch Param](../features/launch-params.md#retrieving-data-in-your-application) key **`"isAppetize": true`.**
{% endhint %}

<img src="../.gitbook/assets/file.excalidraw (3).svg" alt="Sample Structure for using a single app for both generating and utilizing the user token." class="gitbook-drawing">

## Passing the Impersonated User to your Embedded App

Once you have the required user information (e.g. user token), proceed with passing it to your embedded app for impersonation. Consider the following options:

### Option 1: Launch Params

#### Webpage

Pass the generated token as a launch parameter when launching your app via Appetize by making use of our [JavaScript SDK](broken-reference) on your webpage.

{% hint style="info" %}
See [Launch Params](impersonation.md#launch-params) for more info.
{% endhint %}

```javascript
await client.setConfig({
    params: {"impersonatedUserToken":"user_token_to_impersonate"},
    ...
})
```

#### App

Update your app to retrieve, interpret and utilize the token passed in order to simulate the target user's identity, roles, and behaviors.

{% tabs %}
{% tab title="Android" %}
<pre class="language-kotlin" data-overflow="wrap"><code class="lang-kotlin">val preferences = applicationContext.getSharedPreferences("prefs.db", Context.MODE_PRIVATE);

val isAppetizeSession = preferences.getBoolean("isAppetize", false)
<strong>val impersonatedUserToken = preferences.getString("impersonatedUserToken", null)
</strong><strong>
</strong><strong>if(isAppetizeSession &#x26;&#x26; impersonatedUserToken != null) {
</strong><strong>   //autenticate the user with the token passed
</strong><strong>   authenticationService.authenticateUserWithToken(impersonatedUserToken)
</strong><strong>}
</strong></code></pre>
{% endtab %}

{% tab title="iOS" %}
<pre class="language-swift" data-overflow="wrap"><code class="lang-swift">let isAppetizeSession = UserDefaults.standard.bool(forKey: "isAppetize")
<strong>let impersonatedUserToken = UserDefaults.standard.string(forKey: "impersonatedUserToken")
</strong>
guard isAppetizeSession, 
      let impersonatedUserToken = impersonatedUserToken else {  return  }

// authenticate the user with the token passed
authenticationService.authenticateUserWithToken(impersonatedUserToken)
</code></pre>
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
Note `authenticationService` is just an example to represent how authentication might work. This should be replaced with the actual implementation in your app.
{% endhint %}

### **Option 2: Deep Linking**

#### Webpage

Pass the generated token via a deep link while your app is running in Appetize by making use of our [JavaScript SDK](broken-reference) on your webpage.

{% hint style="info" %}
See [Deep Links](../features/deep-links.md) for more info.
{% endhint %}

```typescript
await session.openUrl("appetize://impersonation/user_token_to_impersonate")
```

#### App

Update your app to retrieve, interpret and utilize the token passed in order to simulate the target user's identity, roles, and behaviors.

{% tabs %}
{% tab title="Android" %}
Add a **new intent filter** for the deep link we specified above. For more information on how to do this, see this [Android](https://developer.android.com/training/app-links/deep-linking) tutorial for more information.

```xml
<intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />
        <data android:scheme="appetize"
              android:host="impersonation"
         />
    </intent-filter>
```

Now you can read out the data once the activity is launched.

```kotlin
override fun onCreate(savedInstanceState: Bundle?) {
    super.onCreate(savedInstanceState)
    setContentView(R.layout.authActivity)

    val action: String? = intent?.action
    val data: Uri? = intent?.data
    // get the impersonationToken
    // unauthenticate existing user
    // authenticate with new user
}
```
{% endtab %}

{% tab title="iOS" %}
Update your **AppDelegate** (or **SceneDelegate** if your app opted into using Scenes) to handle incoming deep links. See this [Apple article](https://developer.apple.com/documentation/xcode/defining-a-custom-url-scheme-for-your-app) for more information.

{% code overflow="wrap" %}
```swift
func scene(_ scene: UIScene, 
           willConnectTo session: UISceneSession, 
           options connectionOptions: UIScene.ConnectionOptions) {

    if let urlContext = connectionOptions.urlContexts.first,  
        urlContext.url.absoluteString.prefix("appetize://impersonation") {
          // get the impersonationToken
          // unauthenticate existing user
          // authenticate with new user
    }
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Best Practices

To ensure a secure and responsible impersonation process, adhere to these best practices.

{% hint style="info" %}
Appetize offers both Public and Private cloud deployments. If you are potentially accessing sensitive data, please contact our [support team](mailto:hello@appetize.io) to ensure you are implementing impersonation in a compliant manner.
{% endhint %}

#### **User Consent and Privacy**

Obtain explicit user consent before performing any impersonation activities. Safeguard user privacy and handle sensitive information appropriately.

#### **Limited Scope**

Impersonate users only when necessary to verify or troubleshoot reported issues. Respect user privacy and avoid misuse of impersonation capabilities. If possible limit impersonation to only be accessible via your internal network.

#### **Documentation and Compliance**

Maintain detailed documentation outlining the impersonation process, including how the token gets generated and passed to the app and any other appropriate security measures. Ensure compliance with relevant regulations.

#### **Auditing and Accountability**

Maintain an audit trail of impersonation activities, including the purpose, duration, and actions performed. This log should be accessible for review and compliance purposes.



