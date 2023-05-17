---
description: >-
  Appetizes deep linking feature can be used to simplify user workflows and
  reduce friction by allowing users to jump directly to relevant content or
  actions.
---

# Deep links

{% hint style="success" %}
Supported Links

* Android AppLinks / iOS Universal Links
* Custom Schema Deeplinks
* Web Links
{% endhint %}

### With Query Parameter

{% hint style="info" %}
This URL will be invoked on launch of the device.
{% endhint %}

Set the deep-link URL by adding the URL encoded `launchUrl` query parameter to your app or embed URL.

```uri
&launchUrl=https%3A%2F%2Fwww.appetize.io
```

See [Query Params Reference](query-params-reference.md#launchurl) for more information.

### With JavaScript SDK

Set the deep-link URL of the device via our JavaScript SDK

#### With Configuration

{% hint style="info" %}
This URL will be invoked on launch of the device.
{% endhint %}

```typescript
await client.config({
    launchUrl: "https://www.appetize.io",
    ...
})
```

See [Configuration](../javascript-sdk/configuration.md#launchurl) for more information.

#### With openUrl()

{% hint style="info" %}
This can be called multiple times after launch of the device.
{% endhint %}

```typescript
await session.openUrl("https://appetize.io")
```

See the [API Reference](../javascript-sdk/api-reference.md#openurl) for more information.
