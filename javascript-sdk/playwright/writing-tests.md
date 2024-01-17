# Writing Tests

Each test will have an [Appetize session](../api-reference.md#session-1) for you to interact with your device (like a [page](https://playwright.dev/docs/pages) in Playwright). You can then assert the app based on some criteria, such as the existence of a UI element, a network request, or do a screenshot test.

## Your first test

Take a look at the following test example:

```javascript
import { test, expect } from '@appetize/playwright'

// reinstall app after each test to reset data
test.afterEach(async ({ session }) => {
    await session.reinstallApp()
})

test('logs in to the app', async ({ session }) => {
    // type username
    await session.tap({ 
        element: { 
            attributes: {
                accessibilityIdentifier: 'username_field' 
            }
        } 
    })
    await session.type('jordan')
    
    // type password
    await session.tap({ 
        element: { 
            attributes: {
                accessibilityIdentifier: 'password_field' 
            }
        } 
    })
    await session.type('secretpassword')
    
    // tap login button
    await session.tap({ 
        element: { 
            attributes: {
                text: 'Login' 
            }
        } 
    })
    
    // assert that an element with 'Hello Jordan' exists on the screen
    await expect(session).toHaveElement({ 
        attributes: {
            text: 'Hello Jordan' 
        }
    })
})
```

This will load a hypothetical app with a login screen. It will tap on the username and password fields, type some credentials, log in, and assert that a UI element with text "Hello Jordan" exists.

## Actions

Each test provides the `session` for your app. You can use [Automation](../automation/) actions here to interact with it as you need.

```javascript
test('scrolls through the news feed', async ({ session }) => {
    await session.swipe({
        position: {
            x: '50%',
            y: '50%',
        },
        gesture: 'up'
    })
})
```

### Sequencing actions

All actions are promises that will await until the interaction has been played on the device. If your action [targets an element](../automation/touch-interactions.md#targeting-elements), Appetize will wait for the element to appear before proceeding, which is helpful when your action results in a change in UI.

```javascript
test('navigates to a settings menu', async ({ session }) => {
    await session.tap({ 
        element: { 
            attributes: {
                text: 'Settings' 
            }
        } 
    })
    
    await session.tap({ 
        element: { 
            attributes: {
                text: 'Notifications' 
            }
        } 
    }) 
})
```

All actions that target an element will wait up to 10 seconds for an element to appear. If you need to wait for an element to appear without interacting on it, you can use [waitForElement()](writing-tests.md#waitforelement)

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

These timeouts are also configurable (see [Timeouts](../automation/touch-interactions.md#timeouts).)

## Assertions

### expect

Playwright uses the [expect](https://jestjs.io/docs/expect) library for assertions. We have added custom async matchers for asserting on application state.

#### toHaveElement

Asserts that an element exists in the current application UI

```javascript
await expect(session).toHaveElement({ 
    attributes: {
        text: 'Hello' 
    }
})
```

It can take additional options to change the behaviour of the assertion:

```javascript
await expect(session).toHaveElement(
    {
        attributes: {
            text: 'Hello',
        }
    },
    {        
        timeout: 10000, // time in ms to wait for element to appear (default 10000)
        matches: 1      // require this amount of elements to be found
    }
)
```

#### not.toHaveElement

Asserts that an element does **not** exists in the current application UI

```javascript
await expect(session).not.toHaveElement(
    {
        attributes: {
            text: 'Hello' 
        }
    },
    {
        // We recommend setting a lower timeout for elements we know will not appear, 
        // as it will spend this time looking for the element.
        timeout: 1000, // time in ms to wait for element to appear (default 10000)
    }
 )
```

### Screenshot comparisons

[toMatchSnapshot()](https://playwright.dev/docs/api/class-snapshotassertions#snapshot-assertions-to-match-snapshot-2) works with [session.screenshot()](../automation/device-commands.md#screenshot), allowing you to do screenshot comparisons of your app.

_Note: screenshot tests are fragile by nature as any change in the UI could cause it to fail. It is always better to assert on a narrow piece of application state, such as_ [_toHaveElement_](writing-tests.md#tohaveelement)_, or on network/debug log output._

```javascript
test('loads the home tab', async ({ sesssion }) => {
    await session.findElement({ attributes: { text: 'Home' } })
    
    const screenshot = await session.screenshot()
    
    await expect(session.data).toMatchSnapshot()
})
```

### Network

An example of how you can assert that a network request was made.

[See documentation for network events](../api-reference.md#on-session)

```javascript
test.use({
    config: {
         proxy: 'intercept',
     }
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
await session.waitForElement({ attributes: { text: "Hello" } })

await session.waitForElement(
    { attributes: { text: "Hello" } }, 
    { 
        matches: 2, // wait for exactly 2 elements to match the selector
        timeout: 10000 // wait a maximum of 10 seconds (default)
    }
)
```

### waitForEvent

Waits for an event to occur

```javascript
const networkEvent = await session.waitForEvent('network')

const requestEvent = await session.waitForEvent('network', event => {
    // resolves only when this condition is met
    return event.type === 'request'
})
```

### waitForTimeout

Waits for the given time to elapse (in ms)

```javascript
await session.waitForTimeout(5000)
```
