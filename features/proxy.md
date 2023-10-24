---
description: >-
  Take control of your network traffic with Appetize's advanced proxy support.
  Effortlessly reroute your traffic for better access control, privacy, and
  security.
---

# Proxy

{% hint style="info" %}
Our current support is limited to HTTP Proxies. When your app makes HTTPS connections, the data remains encrypted despite the unencrypted connection to the proxy. The app sends a CONNECT request to the proxy for the destination HTTPS server, initiating an SSL handshake. The proxy acts as a TCP connection forwarder, ensuring end-to-end encryption for app data.
{% endhint %}

## App Level Proxy

Appetize supports settings a proxy server on a per-app basis.

{% hint style="warning" %}
App-Level proxy settings will override the Account **`default proxy`**. if you _always_ want the Account-level proxy to be used, use **`forced proxy`** instead.
{% endhint %}

To allow Appetize to proxy all the network events, you need to specify a proxy server to route network traffic to:

### With Query Parameter

Add the `proxy` query parameter to your app or embed URL with your URL encoded proxy server's address (e.g. `http://example.com:8080/`)as value.

```uri
&proxy=http%3A%2F%2Fexample.com%3A8080%2F
```

See [Query Params Reference](query-params-reference.md#proxy) for more information.

### With JavaScript SDK

Set `proxy` to `http://example.com:8080/` in the configuration e.g.

```typescript
await client.config({
    proxy: "http://example.com:8080",
    ...
})
```

See [Configuration](../javascript-sdk/configuration.md#proxy) for more information.

## Account Level Proxy

{% hint style="info" %}
Account Level Proxy is only available on our Premium and Enterprise plans. [Contact us](https://appetize.io/contact-us) to learn more.
{% endhint %}

You may also set account-wide proxy settings on your [Account](https://appetize.io/account).

### Default Proxy

By setting a default proxy, the proxy will be used when no other proxy is specified.

<figure><img src="../.gitbook/assets/image (3) (3).png" alt="" width="563"><figcaption><p>Example default proxy</p></figcaption></figure>

### Forced Proxy

By setting a forced proxy, the proxy will be used regardless of other proxy settings.

<figure><img src="../.gitbook/assets/image (10).png" alt="" width="563"><figcaption><p>Example forced proxy</p></figcaption></figure>
