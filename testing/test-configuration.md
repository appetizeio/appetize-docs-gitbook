---
description: Run your tests against multiple device configurations
---

# Test Configuration

The Appetize session configuration lives under `use.config` in `playwright.config.ts`. It accepts the same values you can set per session anywhere else — see the [JavaScript SDK configuration](https://docs.appetize.io/javascript-sdk/configuration) reference for the full list.

{% code title="playwright.config.ts" %}
```typescript
use: {
    config: {
        buildId: '<your build id>',
        device: 'iphone15pro',
        osVersion: '18.2',
        language: 'fr',
    },
}
```
{% endcode %}

{% hint style="info" %}
`buildId` was previously called `publicKey`. Both still work, but `buildId` is the current name.
{% endhint %}

## Changing configuration for a suite

`test.use` overrides the config for a file or a `describe` block. Changing config starts a new session, so keep it at the top of the suite rather than inside individual tests.

```javascript
import { test, expect } from '@appetize/playwright'

test.use({
  config: {
    device: 'nexus5',
  },
});

test('app works on nexus5', async ({ session }) => {
  // ...
})
```

Unlike projects, `test.use` **merges** onto the config it inherits, so you only need to name what changes.

See the [Playwright documentation](https://playwright.dev/docs/test-use-options) for more on `test.use`.

## Reading the configuration

The resolved config for the current test is available as an argument:

```javascript
test('my test', async ({ session, config }) => {
   if (config.osVersion === '7.0') {
      // do os 7.0 specific behaviour
   }
})
```

You can also use it to skip tests:

```javascript
test.describe('iOS 16 features', () => {
    // skip suite if osVersion is less than 16
    test.skip(({ config }) => parseInt(config.osVersion) < 16);

    test('some feature', async ({ session }) => { /* ... */ })
})
```

## Running against several configurations

To run your suite against more than one device, OS version or app, see [Projects](https://docs.appetize.io/testing/projects).
