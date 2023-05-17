---
description: >-
  Our Javascript SDK offers an API to programmatically interact with Appetize
  devices. This allows you to automate interactions with the device, verify app
  behavior, and more.
---

# Getting Started

## Installation

First, load the Javascript SDK by adding the following snippet to the `head` section of your page:

```html
<script>
(function () {const n = window,i = document,o = i.getElementsByTagName("script")[0],t = i.createElement("script");
(t.src = "https://js.appetize.io/embed.js"), (t.async = 1), o.parentNode.insertBefore(t, o);
const s = new Promise(function (e) {t.onload = function () {e();};});n.appetize = {getClient: function (...e) {
return s.then(() => n.appetize.getClient(...e));},};})();
</script>
```

The Javascript SDK exposes `window.appetize.getClient(selector)`. It takes a query selector for the embedded iframe (which we will add next) and returns a promise that resolves with a client instance.

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

For sake of example we gave the iframe an id of `appetize`, but it can be anything you wish.

## Starting a Session

Get the client by calling `window.appetize.getClient(selector)`. After getting the client, you can start the session:

```javascript
window.appetize.getClient("#appetize").then(async client => {
    // listen for new session
    // this event will fire whether the session is started programmatically
    // or when the user clicks
    client.on("session", session => {
        console.log('session started!')
    })
    
    // start a session programmatically
    const session = await client.startSession()
})
```

Next we'll cover various ways you can configure the embed, such as the device or OS version.
