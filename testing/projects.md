# Projects

A Playwright [project](https://playwright.dev/docs/test-projects) is a named configuration your tests run under. With Appetize each project carries its own session `config`, so one project can be an iPhone and another a Pixel — running the same tests, or different ones.

{% hint style="warning" %}
A project's `config` **replaces** the one in the top-level `use`; it does not merge with it. If you set `buildId` at the top level only, any project that defines its own `config` fails to start with `Appetize buildId not set`. Give every project a complete config — the examples below share one with a spread.
{% endhint %}

## One app, two platforms

Tests in `tests/ios` run on an iPhone, tests in `tests/android` run on a Pixel.

{% code title="playwright.config.ts" %}
```typescript
import { defineConfig } from '@playwright/test';
import { AppetizeTestOptions } from '@appetize/playwright';

// shared by every project
const app = { buildId: '<your build id>' };

export default defineConfig<AppetizeTestOptions>({
    testDir: './tests',
    timeout: 120 * 1000,
    workers: 1,
    fullyParallel: false,
    use: { baseURL: 'https://appetize.io' },
    projects: [
        {
            name: 'ios',
            testDir: './tests/ios',
            use: { config: { ...app, device: 'iphone15pro' } },
        },
        {
            name: 'android',
            testDir: './tests/android',
            use: { config: { ...app, device: 'pixel7' } },
        },
    ],
});
```
{% endcode %}

```
tests/
├── ios/
│   └── smoke.spec.ts
└── android/
    └── smoke.spec.ts
```

If your iOS and Android builds are separate apps, give each project its own `buildId` instead of sharing one:

```typescript
projects: [
    {
        name: 'ios',
        testDir: './tests/ios',
        use: { config: { buildId: '<ios build id>', device: 'iphone15pro' } },
    },
    {
        name: 'android',
        testDir: './tests/android',
        use: { config: { buildId: '<android build id>', device: 'pixel7' } },
    },
]
```

## One suite, several devices

Leave `testDir` off a project and it runs your whole suite.

```typescript
const app = { buildId: '<your build id>' };

projects: [
    { name: 'pixel7', use: { config: { ...app, device: 'pixel7' } } },
    { name: 'pixel6', use: { config: { ...app, device: 'pixel6' } } },
]
```

The same shape covers OS versions. See [Devices & OS Versions](https://docs.appetize.io/features/devices-and-os-versions) for the versions each device offers.

```typescript
const app = { buildId: '<your build id>', device: 'iphone15pro' };

projects: [
    { name: 'ios-18', use: { config: { ...app, osVersion: '18.2' } } },
    { name: 'ios-17', use: { config: { ...app, osVersion: '17.2' } } },
]
```

## Running them

```bash
# every project
npx playwright test

# one project
npx playwright test --project=android

# what would run, and under which project
npx playwright test --list
```

```
Listing tests:
  [ios] › ios/smoke.spec.ts:3:5 › app launches
  [android] › android/smoke.spec.ts:3:5 › app launches
Total: 2 tests in 2 files
```

Projects run one after another until you raise `workers`. Each worker holds one Appetize session, so keep `workers` at or below the concurrency your plan allows.

```typescript
workers: 2,   // two projects at a time, two concurrent sessions
```

## Reading the project inside a test

The resolved config for the current project is available as a test argument, which is useful for branching or skipping:

```javascript
import { test, expect } from '@appetize/playwright'

test('platform specific', async ({ session, config }) => {
    if (config.device.startsWith('iphone')) {
        // iOS only behaviour
    }
})

test.describe('iOS 18 features', () => {
    test.skip(({ config }) => parseFloat(config.osVersion) < 18);

    test('some feature', async ({ session }) => { /* ... */ })
})
```
