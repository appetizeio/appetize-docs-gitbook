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

### Playwright Config

You will need to update `playwright.config.ts` so that it's configured for Appetize. Update it to the following:

```javascript
const config = {
    testDir: './tests',
    outputDir: 'test-results/',
    timeout: 120 * 1000,
    expect: {        
        timeout: 5000,
        
        // recommended ratio for screenshot testing
        toMatchSnapshot: {
            maxDiffPixelRatio: 0.05,
        }
    },    
    forbidOnly: !!process.env.CI,
    retries: process.env.CI ? 3 : 0,
    reporter: 'line',
    
    // correlates to number of concurrent Appetize sessions at once.
    // if you are a paid Appetize user you may increase this.
    workers: 1,
    
    // required - each test file will use 1 browser and 1 Appetize session
    fullyParallel: false,
    
    use: {    
        trace: 'on-first-retry',
        baseURL: 'https://appetize.io',
    },

    // any browser is fine, but use only 1
    projects: [
        {
            name: 'chromium',
            use: {
                ...devices['Desktop Chrome'],
            },
        }
    ]    
}

export default config;
```

## Usage

Delete the example test files that Playwright made when you generated the project and instead create an `app.spec.ts` file in your tests folder with the following contents:

```javascript
import { test, expect } from '@appetize/playwright'

test.setup({
    // replace with your app's publicKey
    publicKey: '<PUBLIC KEY>'
})

test('loads the home screen', async ({ session }) => {
    await expect(session).toHaveElement({
        // replace with text that appears on your app
        // (case sensitive, must match text string fully)
        text: 'Welcome',
    })
})
```

Once you've updated the test file for your app, run the test with:

```bash
npx playwright test --headed

# or, headlessly

npx playwright test
```

You should see your app load and the test run! The next section will cover what exactly is happening here in detail.
