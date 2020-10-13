# Embed your app

Many customers embed the Appetize.io virtual devices into their own websites and products. You may use an iFrame to embed your app into any HTML. All of the same query parameters described in [Playback options](playback-options.md) are supported.

Simply replace _https://appetize.io/**app**/&lt;publicKey&gt;_ with _https://appetize.io/**embed**/&lt;publicKey&gt;_ to generate a clean link you can embed into your website as an iFrame. 

```markup
<iframe
  src="https://appetize.io/embed/<PUBLIC KEY>?device=iphone8"
  width="378px" height="800px" frameborder="0" scrolling="no"></iframe>
```



