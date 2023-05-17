---
description: >-
  With Launch Params, you can pass custom data to your mobile apps while running
  in Appetize. It can be useful to load custom content, skip onboarding,
  auto-login a specified user, or custom tracking.
---

# Launch Params

## Passing Data to your Application

### With Query Parameter

Set the params data to pass to your application. The data needs to be an URL-Encoded JSON Object e.g.

```json
&params={"foo":"bar"}
```

should be encoded to

```url
&params=%7B%22foo%22%3A%22bar%22%7D
```

See [Query Params Reference](query-params-reference.md#params) for more information.

### With JavaScript SDK

Send the params data to pass to your application as part of the configuration. The data needs to be a JSON Object e.g.

```typescript
await client.config({
    params: {"foo":"bar"},
    ...
})
```

See [Configuration](../javascript-sdk/configuration.md#params) for more information.

## Retrieving Data in your Application

{% hint style="info" %}
For convenience, we set the key **`"isAppetize": true`** while streaming your app to allow you to easily detect if your app is running in Appetize.
{% endhint %}

{% tabs %}
{% tab title="Android (Java)" %}
#### With Intents

The data will be passed as extras into the intent that launches your app, accessible by calling the appropriate get method (based on type) e.g.

```java
Intent intent = getIntent()
intent.getBooleanExtra("isAppetize", false);
intent.getStringExtra("stringKey");
...
```

#### With SharedPreferences

The data will also be stored in SharedPreferences under a file called `prefs.db`. This is accessibly by fetching that `SharedPreferences` instance and calling the appropriate get method e.g.

{% code overflow="wrap" %}
```java
SharedPreferences preferences = getApplicationContext().getSharedPreferences("prefs.db", Context.MODE_PRIVATE);
preferences.getBoolean("isAppetize", false);
preferences.getString("stringKey", null);
...
```
{% endcode %}
{% endtab %}

{% tab title="Android (Kotlin)" %}
#### With Intents

The data will be passed as extras into the intent that launches your app, accessible by calling the appropriate get method (based on type) e.g.

```kotlin
intent.getBooleanExtra("isAppetize", false)
intent.getStringExtra("stringKey")
...
```

#### With SharedPreferences

The data will also be stored in SharedPreferences under a file called `prefs.db`. This is accessibly by fetching that `SharedPreferences` instance and calling the appropriate get method e.g.

{% code overflow="wrap" %}
```kotlin
val preferences = applicationContext.getSharedPreferences("prefs.db", Context.MODE_PRIVATE);
preferences.getBoolean("isAppetize", false)
preferences.getString("stringKey", null)
...
```
{% endcode %}
{% endtab %}

{% tab title="iOS (ObjC)" %}
The data passed will be stored in the shared defaults object, accessible by calling the appropriate method (based on type) e.g.

```objectivec
[[NSUserDefaults standardUserDefaults] boolForKey:@"isAppetize"]
[[NSUserDefaults standardUserDefaults] objectForKey:@"objectKey"]
[[NSUserDefaults standardUserDefaults] stringForKey:@"stringKey"]
...
```
{% endtab %}

{% tab title="iOS (Swift)" %}
The data passed will be stored in the shared defaults object, accessible by calling the appropriate method (based on type) e.g.

```swift
UserDefaults.standard.bool(forKey: "isAppetize")
UserDefaults.standard.object(forKey: "objectKey")
UserDefaults.standard.string(forKey: "stringKey")
...
```
{% endtab %}
{% endtabs %}
