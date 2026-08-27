---
description: >-
  Pass arguments to an iOS app at launch and read them with ProcessInfo or
  UserDefaults.
---

# Launch Arguments

## Passing Data to your Application

Launch arguments pass strings to your iOS app when it starts. For example, pass `-userId`, `123` to provide a user ID.

### With Query Parameter

Set the `launchArgs` data to pass to your application. The data must be a URL-encoded JSON array of strings:

```url
&launchArgs=%5B%22-userId%22%2C%22123%22%5D
```

This decodes to:

```json
["-userId", "123"]
```

See [#launchargs](../platform/query-params-reference.md#launchargs "mention") for more information.

### With JavaScript SDK

Send `launchArgs` to your application as part of the configuration:

```javascript
await client.setConfig({
    launchArgs: ["-userId", "123"],
    // Rest of the configuration
})
```

See [#launchargs](../javascript-sdk/configuration.md#launchargs "mention") for more information.

## Retrieving Data in your Application

{% hint style="info" %}
Launch arguments never persist data. They apply only to the current launch.
{% endhint %}

{% tabs %}
{% tab title="UserDefaults" %}
To read values with `UserDefaults`, pass each value as a `-key`, `value` pair. The key must start with `-`.

```swift
let userId = UserDefaults.standard.string(forKey: "userId")
```

These values use the volatile [argument domain](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/UserDefaults/AboutPreferenceDomains/AboutPreferenceDomains.html). They do not write to persistent `UserDefaults`. They override stored values with the same key for this launch.
{% endtab %}

{% tab title="ProcessInfo" %}
Read any launch arguments with `ProcessInfo.processInfo.arguments`.

```swift
let arguments = ProcessInfo.processInfo.arguments

if let index = arguments.firstIndex(of: "-userId"),
   arguments.indices.contains(index + 1) {
    let userId = arguments[index + 1]
}
```
{% endtab %}
{% endtabs %}

For iOS values read through `UserDefaults`, launch arguments provide a faster launch than [launch-params.md](launch-params.md "mention").
