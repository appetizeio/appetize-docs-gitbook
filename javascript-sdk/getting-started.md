# Getting Started

## Overview

{% hint style="info" %}
The Javascript SDK is **currently in beta** and is subject to breaking changes.
{% endhint %}

Our Javascript SDK offers an API to programmatically interact with Appetize devices. This allows you to automate interactions with the device, verify app behavior, and more.

## Installation

First, load the Javascript SDK by adding the following snippet to the `head` section of your page:

```html
<script>
  !function(b,c,d,a,e,f){a=new Promise(function(g){b[d]={getClient:function(h){
  return e||((e=document.createElement(c)).src="https://js.appetize.io/embed.js",
  e.async=1,(f=document.getElementsByTagName(c)[0]).parentNode.insertBefore(e,f),
  e.onload=function(){g(b[d].getClient(h))}),a}}})}(window,"script","appetize")
</script>
```

The Javascript SDK exposes `window.appetize.getClient(selector)`. It takes a query selector for the embedded iframe (which we will add next) and returns a promise that resolves with a client instance.

### Embed your app

Add an iframe with an [Appetize embed URL](https://docs.appetize.io/core-features/embed-your-app):

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
    const session = await client.startSession()
    console.log('session started!') 
})
```

Next we'll cover various ways you can configure the embed, such as the device or OS version.
