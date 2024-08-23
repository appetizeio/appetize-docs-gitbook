---
description: Getting Started with Appetize AppRecorder and Playwright
---

# Getting Started

You can follow along with the installation steps below to start a new project, or you can clone the [example project here.](https://github.com/appetizeio/appetize-js-sdk-examples/tree/main/playwright-testing)

## Installation

Get started by installing Playwright with Appetize using **npm:**

```sh
npm init @appetize/playwright@latest
```

Run the install command and select the following to get started:

* Your Appetize App's [**buildId**](#user-content-fn-1)[^1]
* The **preferred default device**

<figure><img src="https://lh7-us.googleusercontent.com/slidesz/AGV_vUdOgTMhY5_mOGlIO1bM1w1FNQjzN7R9tfbQ8ItN0DnHyeVeA-8b94lKG71uxzWDcOZwnDf5tpGP8TpfS_lGwVgNACY3eXtKx4Ku0XhW61hoMbQXc8QvUmoexW21LJRtwCcNguKCcfeZgoqc9XLOIzYfQTYWzKox=nw?key=Ov-qIhkbe_J50OTU5jQN9g" alt="" width="563"><figcaption></figcaption></figure>

## What's Installed <a href="#whats-installed" id="whats-installed"></a>

* A Playwright project will be created  (see [Playwright documentation](https://playwright.dev/docs/intro#installing-playwright)).
* The `@appetize/playwright` npm package will be installed.
* The `playwright.config.ts` file will be configured for Appetize with the specified values for the default device and app. &#x20;

{% hint style="info" %}
See [Test Configuration](test-configuration.md) for more advanced configurations.
{% endhint %}

* An example test file, `app.spec.ts`, will be added.

## Usage

Update the `app.spec.ts` file in your tests folder to include a test relevant to your application

```javascript
import { test, expect } from '@appetize/playwright'

test('example test', async ({ session }) => {
    await expect(session).toHaveElement({
         attributes: {
          // replace with the text of an element that appears on your app
            text: 'Hello world' 
        }
    })
})
```

Once you've updated the test file for your app, run the test with:

```bash
npx playwright test --headed

# or, headlessly

npx playwright test
```

## Next Steps

{% content-ref url="writing-tests.md" %}
[writing-tests.md](writing-tests.md)
{% endcontent-ref %}

{% content-ref url="test-configuration.md" %}
[test-configuration.md](test-configuration.md)
{% endcontent-ref %}

[^1]: previously known as **publicKey**
