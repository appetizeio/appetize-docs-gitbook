---
description: >-
  With Appetize, you can capture, inspect, validate and troubleshoot all network
  traffic (including any API calls) occurring during your app session for
  real-time or later analysis.
---

# Network Traffic Monitor

{% hint style="warning" %}
Note by default, a user needs to be authenticated to view network traffic using the built-in intercept proxy. See [App Permissions](../platform/app-management/app-permissions.md) for more information.
{% endhint %}

## Capture Network Traffic

To allow Appetize to capture all network events, you need to set the proxy of the device to `intercept`.

### With Query Parameter

Add the `proxy` query parameter to your app or embed URL with `intercept` as value.

```uri
&proxy=intercept
```

See [Query Params Reference](../platform/query-params-reference.md#proxy) for more information.

### With JavaScript SDK

Set `proxy` to `intercept` in the configuration e.g.

```typescript
await client.setConfig({
    proxy: "intercept",
    ...
})
```

See [Configuration](../javascript-sdk/configuration.md#proxy) for more information.

## Inspecting Network Traffic

### With App Page

The app page provides a simple network log of all the events that took place. You can access this via your app's app link

{% code overflow="wrap" %}
```url
https://appetize.io/app/{appId|buildId|publicKey}?&proxy=intercept
```
{% endcode %}

or by going to your [Apps](https://appetize.io/apps) page, selecting the app you want to inspect, and then clicking `debug` on the latest build or choosing a specific build you would like to debug.

<figure><img src="../.gitbook/assets/image (22).png" alt=""><figcaption><p>Select <code>Debug</code> for the app or a specific build</p></figcaption></figure>

{% hint style="info" %}
You can also open the network logs in Chrome DevTools if you are running the app in a Chrome Browser by selecting the `Chrome DevTools` button.

Alternatively you can download the HAR file and open it in your favorite Network Monitoring tool.
{% endhint %}

<figure><img src="../.gitbook/assets/Screenshot 2023-10-26 191724.png" alt="Example App Network Event Log"><figcaption><p>Network log tab with associated action buttons for downloading the HAR or opening in Chrome DevTools</p></figcaption></figure>

### With JavaScript SDK

You can listen for all network events via our JavaScript SDK. To easily view them in the browser you can print them to the console or you can store it to file for later analysis

```typescript
session.on('network', (data) => {
    // intercepted network request
    if (data.type === 'request') {
        console.log(`[${data.request.method}]: ${data.request.url}`)
    } 
    
    // intercepted network response
    if (data.type === 'response') {
        console.log(data.response.postData)
    }
})
```

See our JavaScript [API Reference](../javascript-sdk/api-reference/#on-1) for more information.

{% hint style="info" %}
[getNetworkInspectorUrl](../javascript-sdk/api-reference/#getnetworkinspectorurl) provides a direct URL for opening network logs in Chrome DevTools
{% endhint %}
