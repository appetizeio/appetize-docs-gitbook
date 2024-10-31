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

Appetize allows configuration of deep links at app launch with[ launchUrl](deep-links.md#launchurl) or during runtime with [openUrl](deep-links.md#openurl), depending on when and how the link needs to be triggered.

## launchUrl

To launch a URL (deep link or regular) when the device starts.

{% hint style="info" %}
Verifies AppLink or Universal Link associations (if applicable), which may delay the device launch until the validation is complete
{% endhint %}

{% tabs %}
{% tab title="Query Parameter" %}
Set the deep-link URL by adding the URL encoded `launchUrl` query parameter to your app or embed URL.

```url
&launchUrl=https%3A%2F%2Fwww.appetize.io
```

See [Query Params Reference](../platform/query-params-reference.md#launchurl) for more information.
{% endtab %}

{% tab title="JavaScript SDK" %}
Set the deep-link URL of the device via our JavaScript SDK

```typescript
await client.setConfig({
    launchUrl: "https://www.appetize.io",
    ...
})
```

See [Configuration](../javascript-sdk/configuration.md#launchurl) for more information.
{% endtab %}
{% endtabs %}

## openUrl

To launch a URL (deep link or regular) while the device (or application) is already running.

{% hint style="info" %}
This can be called multiple times after launch of the device, with the assumption that all AppLink and Universal Link associations are already established.
{% endhint %}

```typescript
await session.openUrl("https://appetize.io")
```

See the [API Reference](../javascript-sdk/api-reference/#openurl) for more information.

## Troubleshooting

{% hint style="warning" %}
Please note that the use of AppLinks and Universal Links may be affected if our network traffic monitor feature is enabled.
{% endhint %}

### Verifying Associated Domains Entitlement included in your iOS App

1. Open the Terminal on your macOS machine.
2. Navigate to the directory where your app's `.app` bundle is located. For example, if your app is named `YourAppName`, and it's in the `/Applications` folder, you can use the following command to change to that directory:

```bash
cd /Applications/YourAppName.app
```

3. Run the `codesign` command with the `--entitlements` flag to extract the entitlements XML from your app bundle:

<pre class="language-bash"><code class="lang-bash"><strong>codesign -d --entitlements - YourAppName.app/
</strong></code></pre>

This command will print the entitlements XML to the Terminal.

4. Verify that the entitlements XML contains the `com.apple.developer.associated-domains` key and that it specifies the expected URL for your associated domain. The output should look like the following:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "https://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
  <dict>
    <key>com.apple.developer.associated-domains</key>
    <array>
      <string>applinks:yourexpected.domain.com</string>
    </array>
  </dict>
</plist>
```

Ensure that the `<string>` value within `<array>` corresponds to the domain you expect for your app's associated domains.
