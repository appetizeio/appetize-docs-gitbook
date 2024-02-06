# Getting Started

You can follow along with the installation steps below to start a new project, or you can clone the [example project here.](https://github.com/appetizeio/appetize-js-sdk-examples/tree/main/playwright-testing)

## Installation

Create a new Playwright project ([see Playwright documentation](https://playwright.dev/docs/intro#installing-playwright))

```bash
npm init playwright@latest
```

Then install `@appetize/playwright`

```bash
npm install @appetize/playwright
```

## Playwright Config

You will need to update `playwright.config.ts` so that it's configured for Appetize. Update it to the following:

```javascript
const config = {
    testDir: './tests',
    outputDir: 'test-results/',
    timeout: 120 * 1000,
    expect: {        
        // recommended ratio for screenshot testing
        toMatchSnapshot: {
            maxDiffPixelRatio: 0.05,
        }
    },
    forbidOnly: !!process.env.CI,
    retries: process.env.CI ? 3 : 0,
    reporter: 'line',
    
    // correlates to number of concurrent Appetize sessions at a time
    workers: 1,
    fullyParallel: false,
    
    use: {    
        trace: 'retain-on-failure',
        baseURL: 'https://appetize.io',
        
        // Appetize session configuration
        config: {
            device: 'iphone14pro',
            publicKey: '<PUBLIC KEY>'
        }    
    },
}

export default config;
```

{% hint style="info" %}
See [Test Configuration](test-configuration.md) for more advanced configurations.
{% endhint %}

## Usage

Delete the example test files that Playwright made when you generated the project and instead create an `app.spec.ts` file in your tests folder with the following contents:

```javascript
import { test, expect } from '@appetize/playwright'

test('loads the home screen', async ({ session }) => {
    await expect(session).toHaveElement({
         attributes: {
          // replace with text of element that appears on your app
            text: 'Welcome' 
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

