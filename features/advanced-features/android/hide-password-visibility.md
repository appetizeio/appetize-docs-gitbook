---
description: >-
  Android sessions on Appetize always hide password visibility, so typed
  password characters are never shown.
---

# Hide Password Visibility

Android sessions always hide password visibility. Password fields show a dot for every character as soon as it's typed, without briefly showing the character itself.

{% hint style="info" %}
The `hidePasswords` query parameter and JavaScript SDK option are no longer needed and have no effect.
{% endhint %}

### Showing typed password characters

To show each typed character briefly, as Android does by default, turn the setting back on with an [`adbShellCommand`](../../../platform/query-params-reference.md#adbshellcommand) that runs when the session starts:

```
settings put system show_password 1; settings put secure show_password_touch 1; settings put secure show_password_physical 1
```

Android 17 and later use `show_password_touch` for the on-screen keyboard and for text typed with the JavaScript SDK, and `show_password_physical` for hardware key input. Earlier versions only read `show_password`.

#### With Query Parameter

Add the URL-encoded command to your app or embed URL

```uri
&adbShellCommand=settings%20put%20system%20show_password%201%3B%20settings%20put%20secure%20show_password_touch%201%3B%20settings%20put%20secure%20show_password_physical%201
```

#### With JavaScript SDK

Set `adbShellCommand` in the configuration e.g.

```typescript
await client.setConfig({
    adbShellCommand:
        'settings put system show_password 1; settings put secure show_password_touch 1; settings put secure show_password_physical 1',
    ...
})
```

See [Configuration](../../../javascript-sdk/configuration.md#adbshellcommand) for more information.
