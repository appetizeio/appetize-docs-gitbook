---
description: >-
  With  a simple import change and a configuration update, you can use your
  existing Playwright tests  to also do native browser testing with the Appetize
  integration
---

# Web Tests on Mobile Browsers

## Prerequisites

Before you begin, make sure you have the following:

* **Preferred Android Device:** You will need one of our [Android devices](../features/devices-and-os-versions.md) with Chrome 87 or higher (Android 13+ is recommended for best results).
* **ADB Installed:** Ensure [Android Debug Bridge (ADB)](https://developer.android.com/tools/adb) is installed on your system.
* **Enable ADB Tunnel:** Enable [ADB tunnel](https://docs.appetize.io/features/advanced-features/android/adb-tunnel#enable-adb-tunnel) on the session used.

## Configuration

If you haven’t set up Appetize with Playwright yet, we recommend look at our [**Getting Started**](getting-started.md) guide. After successfully integrating Appetize, open the `playwright.config.ts` file to configure the settings for your desired device for native browser testing. If you are already using Playwright for web testing, you can easily add a new project as shown below.

For the **buildId**, we suggest using your [device's sandbox](https://appetize.io/standalone) ID, which can be found in the URL bar. Look for the identifier that starts with `standalone_***` and use that as your buildId. Here’s an example configuration:

```typoscript
{
    name: 'Appetize Native Browser Test',
    use: {
        config: {
                device: 'pixel7',
                osVersion: '13',
                publicKey: 'standalone_***',
                enableAdb: true
        }
    }
}
```

## Page Fixture

The Appetize integration overrides the default page fixture to automatically determine when to use a standard browser (e.g., Chrome or Firefox) versus a native device browser for testing. This means all the logic is handled for you, simplifying the testing process.

### Update your imports

To get started, simply update your imports. Change your Playwright import for `test` to the Appetize version:

From:

```typescript
import { test } from '@playwright/test';
```

To:

```typescript
import { test } from '@appetize/playwright';
```

### Run your tests

{% content-ref url="running-tests.md" %}
[running-tests.md](running-tests.md)
{% endcontent-ref %}

