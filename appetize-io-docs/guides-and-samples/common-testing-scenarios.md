---
description: >-
  Test mobile apps with Appetize and Playwright. This guide covers common
  scenarios like biometric validation, network request interception, and deep
  link testing, as well as working with hardware featu
---

# Common testing scenarios

## Overview

This document assumes you have already set up an Appetize Playwright project. If not, we recommend reading the [Playwright Testing for Mobile documentation](../testing/).

In this section, we'll cover several scenarios you might encounter, and how to solve them, while writing end-to-end integration tests using Appetize and Playwright. These use cases include hardware-related features like biometry validation, event listeners like intercepting network requests, and specific app functionality like testing deep links.

## Scenarios

### Change location and language

Developing localization testing can be a challenging and complex scenario to set up. These tests are relevant since some functionalities apply to specific areas.

The [Mock Location](../features/mock-location.md) and [Language & Locale](../features/language-and-locale.md) documentation pages provides an example of how to implement it using our JS SDK. Sometimes you may wan't to change the location and language for all test cases, pass the configuration as an option of the [test.use](https://playwright.dev/docs/api/class-test#test-use) method from playwright to achieve it.

```typescript
import { test } from '@appetize/playwright';

const madridLocation = [40.451975, -3.688530] // Latitude, longitude
const language = 'en_US'

// Set all test cases in this scope to mock the location to be in Madrid
test.use({
  config: {
    location: madridLocation,
    language,
  },
});
```

### Clear the application state between tests

Independent state for each one of the test scripts is critical to have reliable runs. The best way to guarantee no trace left of any data related to the installed application from previous runs is to re-install the application after each test. Declare in the tests this behavior by utilizing the [reinstallApp](../javascript-sdk/api-reference/#reinstallapp) method inside the [afterEach hook](https://playwright.dev/docs/api/class-test#test-after-each) from Playwright.

```typescript
import { test } from '@appetize/playwright';

// Reinstall app after each test to reset data
test.afterEach(async ({ session }) => {
    await session.reinstallApp()
});
```

### Test Deep Links inside the application

Deep Links and Universal/App Links play a critical role in mobile application functionality. To open and test any URL that your application supports in a test script, use the [openUrl](../javascript-sdk/api-reference/#openurl-url) method to trigger a Deep Link or the [launchUrl](../javascript-sdk/configuration.md#launchurl) configuration property to invoke it at launch and validate that the expected view is visible after handling the link. For more information, visit the [Deep Links](../features/deep-links.md) section from the documentation.

{% hint style="info" %}
[Auto-grant permissions](../features/auto-grant-permissions.md) allow to automatically trust incoming Deep Links that the application can handle.
{% endhint %}

```typescript
import { test } from '@appetize/playwright';
// Allow deep links to be trusted by default
test.use({
  config: {
    grantPermissions: true
  },
});

test('Check my deep link view is displayed', ({ session }) => {
    // Open the deeplink
    await session.openUrl('sampleApp://myDeepLink1');
    
    // Wait for the view to be stabilized
    await session.waitForAnimations();
    
    // Assert the view is displayed
    await expect(session).toHaveElement({
        attributes: {
            text: 'This is your deep link 1 view! 🎉',
        },
    });
});
```

### Analytics tests

Analytics in mobile development allow us to understand how the application is being used or the effectiveness of a new feature. The validation of analytics events is a common scenario to test that can get complicated as your application grows.

Network assertions allows to seamlessly validate an analytic event has been triggered, using the [network validation example](../testing/writing-tests.md) from our docs we can adapt the code to validate that a request with an specific url contains the event in the body.

```typescript
// request.postData.text is string representation. 
// If the mimetype is application/json you'll get the encoded json.
const body = JSON.parse(request.postData.text)
expect(body).toContainEqual({
    eventId: '<id of the event to validate>',
    metadata: //{ ...etc },
})
```

### Validate biometric user journey

Face ID, Touch ID, or any other biometrics validation is one of the critical features that mobile applications must test. A typical approach to test these features would be to have a service class for biometrics validation/enrollment and mock the result inside your tests with dependency injection. This approach can become complex to maintain as your application grows and does not offer full test coverage. Use the [biometry](../javascript-sdk/automation/device-commands.md#biometry) method to mock a biometrics match result without requiring additional setup.

```typescript
import { test } from '@appetize/playwright';

test('Check card is displayed after a successful biometrics match', ({ session }) => {
    // Navigate to the card details in our application
    await session.tap({
        element: {
            attributes: {
                'text': "Show card details 💳"
            }
        }
    });
    // Wait for the view to be stabilized
    await session.waitForAnimations();
    // Pass biometric verification
    await session.biometry({
        match: true
    });
    
    // Validate biometric enabled and credit card is displayed
    await expect(session).toHaveElement({
      attributes: {
        text: "Card number xxxx-xxxx-xxxx-xxxx",
      },
    });
})
```

### UI Branded Components Comparison

Ensuring consistency in the UI of the application can be challenging. An example of this is branded/flavored UI components, where validating that each one of the components looks as expected and there was no regression is vital. To solve this with Appetize do [screenshot comparisons](../testing/writing-tests.md#screenshot-comparisons) and validate the UI.

{% hint style="info" %}
We recommend using maxDiffPixelRatio option instead of maxDiffPixels to avoid flaky tests. For more information on the options available visit the [Playwright SnapshotAssertions](https://playwright.dev/docs/api/class-snapshotassertions#snapshot-assertions-to-match-snapshot-2) documentation.
{% endhint %}

```typescript
import { test } from '@appetize/playwright';

test('Check dark flavor of component', () => {
    await this.session.waitForAnimations();
    
    await session.openUrl('whitelabel://component?type=dark');
    
    // Take the screenshot and save it as a buffer
    const screenshot = await session.screenshot('buffer')
    expect(screenshot.data).toMatchSnapshot({
        name: 'component-dark.png',
        maxDiffPixelRatio: 0.05 // Allow 5% of the pixels to be different
    });
});
```
