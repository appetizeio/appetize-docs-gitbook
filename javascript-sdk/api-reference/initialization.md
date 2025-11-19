---
description: Obtain an Appetize client instance using one of the getClient methods.
---

# Initialization

## getClient(selector)

Get an instance of the Appetize client.

{% hint style="warning" %}
When using `getClient(selector)`, you **must set** the iframe’s `src` attribute _before_ calling `getClient` to configure the initial session.
{% endhint %}

```javascript
const client = await window.appetize.getClient('#my_iframe')
```

**Parameters**

| Name     | Type     | Description                                             |
| -------- | -------- | ------------------------------------------------------- |
| selector | `string` | A query selector string pointing to the embedded iframe |

## getClient(selector, config)

Get an instance of the Appetize client as well as set the initial config when loading the client.

_Useful when the embed link might not be known up front and the configuration has to be applied at runtime._

{% hint style="warning" %}
When using `getClient(selector, config)`, **do not set** `iframe.src`.\
Setting the `src` manually may cause a race condition where the iframe loads before the SDK connects.\
\
For Private Cloud embeds, use `data-appetize-url` on the iframe instead of `src`.
{% endhint %}

```javascript
const client = await window.appetize.getClient('#my_iframe', {
    buildId: '{buildId|publicKey}',
    device: 'iphone11pro',
    osVersion: '15.0'
    ...
})
```

**Parameters**

| Name     | Type                                    | Description                                                                                                     |
| -------- | --------------------------------------- | --------------------------------------------------------------------------------------------------------------- |
| selector | `string`                                | A query selector string pointing to the embedded iframe                                                         |
| config   | [SessionConfig](types/sessionconfig.md) | A JSON object describing the [Configuration options](../configuration.md#configuration-options) for the device. |
