---
description: >-
  Enhance your user experience by embedding  Appetize virtual devices into your
  own website or product using Appetize's embedding functionality.
---

# Embedding Apps

Many customers embed the Appetize virtual devices into their own websites and products. You may use an `iFrame` to embed your app into any HTML.&#x20;

Our embed links support all our [Query Parameters](../features/query-params-reference.md) to allow you to fully customize your experience.

## Where is my embed link?

The easiest way to find your embed link is by going to your [Apps](https://appetize.io/apps) page and selecting `embed` under the app you want to embed on your website.

<figure><img src="../.gitbook/assets/image (10) (1) (1) (4).png" alt="" width="366"><figcaption><p>Select "embed" under your app</p></figcaption></figure>

You can also simply replace **app** with **embed** in the your app's app link (see [Running Apps](running-apps.md)) e.g.&#x20;

```
https://appetize.io/app/{publicKey}
```

will become

```
https://appetize.io/embed/{publicKey}
```

{% hint style="info" %}
You can customize and test out all the [Query Parameters](../features/query-params-reference.md) on your [App Page](running-apps.md) before switching out the `app` link with an `embed` link.
{% endhint %}

## Sample Usage

After obtaining the embed link, you can easily embed the content into your website by creating an `iFrame`:

{% code overflow="wrap" %}
```html
<iframe
  src="https://appetize.io/embed/{publicKey}"
  width="378px" 
  height="800px" 
  frameborder="0" 
  scrolling="no"></iframe>
```
{% endcode %}
