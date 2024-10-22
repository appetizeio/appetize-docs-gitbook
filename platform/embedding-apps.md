---
icon: code
description: >-
  Enhance your user experience by embedding  Appetize virtual devices into your
  own website or product using Appetize's embedding functionality.
---

# Embedding

Many customers embed the Appetize virtual devices into their own websites and products. You may use an `iFrame` to embed your app into any HTML.

Our embed links support all our [Query Parameters](query-params-reference.md) to allow you to fully customize your experience.

## Where is my embed link?

The easiest way to find your embed link is by going to your [Apps](https://appetize.io/apps) or [App Builds](app-management/listing-apps.md#app-builds-page) page and selecting **share** under the app, App Group or build that you want to embed on your website.

<figure><img src="../.gitbook/assets/image (38).png" alt="" width="371"><figcaption><p>Find your embed link by clicking the share button</p></figcaption></figure>

Currently, `Share` will share a specific build of your application. Soon, we will introduce new sharing features that will allow you to share the latest build without changing the URL.

<figure><img src="../.gitbook/assets/image (17).png" alt="" width="386"><figcaption><p>Example Share dialog</p></figcaption></figure>

{% hint style="info" %}
You can customize and test out all the [Query Parameters](query-params-reference.md) on your [App Page](app-management/running-apps.md) before switching out the `app` link with an `embed` link.
{% endhint %}

## Sample Usage

After obtaining the embed link, you can easily embed the content into your website by creating an `iFrame`:

{% code overflow="wrap" %}
```html
<iframe
  src="https://appetize.io/embed/{buildId}"
  width="378px" 
  height="800px" 
  frameborder="0" 
  scrolling="no"></iframe>
```
{% endcode %}
