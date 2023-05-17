# Writing Tests

Each test will have an [Appetize session](../automation/) for you to interact with your device (like a [page](https://playwright.dev/docs/pages) in Playwright). You can then assert the app based on some criteria, such as the existence of a UI element, a made network request, or a screenshot.

## Your first test

Take a look at the following test example:

```javascript
import { test, expect } from '@appetize/playwright'

test.setup({
    publicKey: '<PUBLIC KEY>',
    // ... other config
    // see https://docs.appetize.io/javascript-sdk/configuration
})

// reinstall app after each test to reset data
test.afterEach(async ({ session }) => {
    await session.reinstallApp()
})

test('logs in to the app', async ({ session }) => {
    // type username
    await session.tap({ element: { accessibilityIdentifier: 'username_field' } })
    await session.type({ value: 'jordan' })
    
    // type password
    await session.tap({ element: { accessibilityIdentifier: 'password_field' } })
    await session.type({ value: 'secretpassword' })
    
    // tap login button
    await session.tap({ element: { text: 'Login' } })
    
    // wait for an element with 'Hello Jordan' to exist on the screen
    await expect(session).toHaveElement({ text: 'Hello Jordan' })
})
```

This will load a hypothetical app with a login screen. It will tap on the username and password fields, type some credentials, log in, and assert that a UI element with text "Hello Jordan" exists.

## Setup

It is required to call `test.setup` at the start of your test suite. It takes a [configuration](../configuration.md) object to specify your publicKey, device, OS version, etc.

Typically you will call this at the top-level of your test file, but you can also nest them under `test.describe()`

```javascript
test.describe('iOS app', () => {
    test.setup({ publicKey: '...', device: 'iphone14pro' })

    test('logs in', async ({ session }) => {
       // ...
    })
})

test.describe('Android app', () => {
    test.setup({ publicKey: '...', device: 'pixel7' })

    test('logs in', async ({ session }) => {
       // ...
    })
})
```

## Actions

Each test provides the `session` for your app. You can use [Automation](../automation/) actions here to interact with it as you need.

```javascript
test('scrolls through the news feed', async ({ session }) => {
    await session.swipe({
        x: '50%',
        y: '50%',
        direction: 'up'
    })
})
```

### Sequencing actions

All actions are promises that will await until the interaction has been played on the device. If your action [targets an element](../automation/touch-interactions.md#targeting-elements), Appetize will wait for the element to appear before proceeding, which is helpful when your action results in a change in UI.

```javascript
test('navigates to a settings menu', async ({ session }) => {
    await session.tap({ element: { text: 'Settings' } })
    await session.tap({ element: { text: 'Notifications' } })    
})
```

If you just need to wait for an element to appear, you can use [waitForElement()](writing-tests.md#waitforelement)

```javascript
test('screenshot of the settings page', async ({ session }) => {
    // tapping on 'Settings' will trigger a screen transition
    await session.tap({ element: { text: 'Settings' } })
    
    // wait for a UI element to appear
    await session.waitForElement({ text: 'Notifications' })
    
    // take a screenshot
    const screenshot = await session.screenshot()
    expect(screenshot.data).toMatchSnapshot()    
})
```

## Assertions

### expect

Playwright uses the [expect](https://jestjs.io/docs/expect) library for assertions. We have added custom async matchers for asserting on application state.

#### toHaveElement

Asserts that an element exists in the current application UI

```javascript
await expect(session).toHaveElement({ text: 'Hello' })
await expect(session).toHaveElement({ accessbilityIdentifier: 'greeting-label' })
```

It can take additional options to change the behaviour of the assertion:

```javascript
await expect(session).toHaveElement(
    {
        text: 'Hello',
    },
    {        
        timeout: 30000, // time in ms to wait for element to appear (default 30000)
        matches: 1      // require this amount of elements to be found
    }
)
```

If you want to assert that an element does **not** exist:

```javascript
await expect(session).not.toHaveElement(
    {
        text: 'Hello',
    },
    // since we expect the element to not exist, it will use up the full timeout
    // and pass as long as it never found anything.
    { timeout: 5000 }
)
```

### Screenshot comparisons

[toMatchSnapshot()](https://playwright.dev/docs/api/class-snapshotassertions#snapshot-assertions-to-match-snapshot-2) works with [session.screenshot()](../automation/device-commands.md#screenshot), allowing you to do screenshot comparisons of your app.

_Note: screenshot tests are fragile by nature because any change in the UI will cause it to fail. It is always better to assert on a narrow piece of application state, such as_ [_toHaveElement_](writing-tests.md#tohaveelement)_, or on network/debug log output._

```javascript
test('loads the home tab', async ({ sesssion }) => {
    await session.findElement({ text: 'Home' })
    
    const screenshot = await session.screenshot()
    
    await expect(session.data).toMatchSnapshot()
})
```

### Network

An example of how you could assert that a network request was made.

[See documentation for network events](../api-reference.md#on-session)

```javascript
test.setup({
 proxy: 'intercept',
 // ... rest of your config
})

test('makes a network request to the API with authentication', async ({ session }) => {
    const { request } = await session.waitForEvent('network', event => {
        if (event.request.url.startsWith('https://api.example.com')) {
            return true;
        }
    })
    
    // request.headers is an array of objects
    expect(request.headers).toContainEqual({
        name: 'Authorization',
        value: expect.stringMatching(/^Basic /),
    })
})

```

## Helpers

`session` contains a few helper methods for writing tests that may come in handy

### waitForElement

Waits for an element to appear.

```javascript
await session.waitForElement({ text: "Hello" })

await session.waitForElement(
    { text: "Hello" }, 
    { 
        matches: 2, // wait for exactly 2 elements to match the selector
        timeout: 30000 // wait a maximum of 30 seconds
    }
)
```

### waitForEvent

Waits for an event to occur

```javascript
const networkEvent = await session.waitForEvent('network')

const requestEvent = await session.waitForEvent('network', event => {
    return event.type === 'request'
})
```

### waitForTimeout

Waits for the given time to elapse (in ms)

```javascript
await session.waitForTimeout(5000)
```
