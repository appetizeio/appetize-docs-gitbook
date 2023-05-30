---
description: Run your tests against multiple device configurations
---

# Test Configuration

## Changing configuration

You can change the configuration for a test suite with `test.use`. Note that config changes will start a new session when used within a `test.describe`.

See [Playwright documentation](https://playwright.dev/docs/test-use-options) for more details on `test.use`.

```javascript
import { test, expect } from '@appetize/playwright'

test.use({
  config: {
    publicKey: '<PUBLIC KEY >'
    device: 'nexus5'
  },
});

test('app works on nexus5', async ({ session }) => {
  ...
})
```

## Getting configuration

The current configuration can be accessed with the `config` argument in the test

```javascript
test('my test', async ({ session, config }) => {
   if (config.osVersion === '7.0') {
      // do os 7.0 specific behaviour
   } else {
      
   }
})
```

You can also use this to skip tests

```javascript
test.describe('iOS 16 features', () => {
    // skip suite if osVersion is less than 16
    test.skip(({ config }) => parseInt(config.osVersion) < 16);
    
    test('some feature', async ({ session }) => { ... })
})
```

## Projects

[Projects](https://playwright.dev/docs/test-projects) allow you to run your entire test suite with different configurations. This is useful if you have a cross platform app or wish to test against a set of devices and/or osVersions.

Below are some examples that may fit your use case.

### Examples

#### Test Android and iOS apps

Runs tests under `tests/ios` for the iOS configuration, and `tests/android` for the Android configuration

```javascript
const config = {
    // ... 
    
    projects: [
        {
            name: 'ios',
            testDir: './tests/ios',
            use: {
                config: {
                    device: 'iphone14pro',
                    publicKey: '<IOS APP PUBLIC KEY>'
                }
            },
        },
        {
            name: 'android',
            testDir: './tests/android',
            use: {
                config: {
                    device: 'pixel6',
                    publicKey: '<ANDROID APP PUBLIC KEY>'
                }
            },
        }      
    ]
} 
   
```

#### Test iOS app against multiple iOS Versions

Runs the test suite against iOS 16 and iOS 15

```javascript
const config = {
    // ... 
    
    use: {
        config: {
            publicKey: '<PUBLIC KEY>'
        }
    },
    projects: [
        {
            name: 'ios-16',
            use: {
                config: {
                    device: 'iphone14pro',
                    osVersion: '16',
                }
            },
        },
        {
            name: 'ios-15',
            use: {
                config: {
                    device: 'iphone14pro',
                    osVersion: '15'
                }
            },
        }
    ]
} 
   
```

#### Test Android against multiple devices

Runs the test suite against a Pixel 7 and a Pixel 6

```javascript
const config = {
    // ... 
    
    use: {
        config: {
            publicKey: '<PUBLIC KEY>'
        }
    },
    projects: [
        {
            name: 'pixel7',
            use: {
                config: {
                    device: 'pixel7'
                }
            },
        },
        {
            name: 'pixel6',
            use: {
                config: {
                    device: 'pixel6'
                }
            },
        }
    ]
}
```

## During tests

You can reference the current project configuration in your tests. This is useful if you need to change or skip a test based on a certain device
