---
description: >-
  Our JavaScript SDK offers an API to programmatically interact with Appetize
  devices. This allows you to automate interactions with the device, verify app
  behavior, and more.
---

# Getting Started

## Installation

First, load the JavaScript SDK by adding the following snippet to the `head` section of your page:

```html
<script>
(function () {const n = window,i = document,o = i.getElementsByTagName("script")[0],t = i.createElement("script");
(t.src = "https://js.appetize.io/embed.js"), (t.async = 1), o.parentNode.insertBefore(t, o);
const s = new Promise(function (e) {t.onload = function () {e();};});n.appetize = {getClient: function (...e) {
return s.then(() => n.appetize.getClient(...e));},};})();
</script>
```

### Embed your app

Add an `iframe` with an [Appetize embed URL](../platform/embedding-apps.md):

```html
<iframe
    id="appetize"
    src="https://appetize.io/embed/<PUBLIC KEY>"
    width="378px" 
    height="800px" 
    frameborder="0" 
    scrolling="no"></iframe>
```

{% hint style="info" %}
We gave the iframe an id of `appetize`, but it can be anything you wish.&#x20;
{% endhint %}

## Get the Client

The easiest way to get the client is by calling [`window.appetize.getClient(selector)`](api-reference.md#getclient-selector).&#x20;

This will return an Appetize client instance for the embed e.g.

```javascript
const client = await window.appetize.getClient("#appetize")
```

{% hint style="info" %}
We also support getting the client with an initial [configuration](configuration.md) - for scenarios where the initial embed link might not be known on launching of the page by making use of [`window.appetize.getClient(selector, config)`](api-reference.md#getclient-selector-config).&#x20;

This will return an Appetize client instance with the initial [configuration](configuration.md) applied e.g.

```javascript
const client = await window.appetize.getClient("#appetize", {
    publicKey: '{publicKey}',
    device: 'iphone13pro',
    osVersion: '15.0'
    ...
})
```
{% endhint %}

## Starting a Session

You can start a session programmatically:

```javascript
const session = await client.startSession()
console.log('session started!')
```

or wait for the user to click "Tap to Play":

```javascript
client.on("session", session => {
    console.log('session started!')
})
```

Next we'll cover various ways you can configure the embed, such as the device or OS version.
