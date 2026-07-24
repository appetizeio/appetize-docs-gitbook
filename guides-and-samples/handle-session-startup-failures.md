---
description: >-
  Show custom UI and recover when an embedded session cannot reach a ready
  state.
---

# Handle session startup failures

## Overview

Use `sessionError` to handle any session that was served but failed to become ready.

The event reports an `Error` with a message and stack trace. Startup failures can have many causes. An invalid configuration is only one example.

Register the listener before requesting a session. Log the full error for diagnostics. Show users a clear recovery action.

## Show a custom error

Use `error` for client-level failures. Use `sessionError` for failures after a session was served.

```typescript
const client = await window.appetize.getClient('#appetize', config)

client.on('error', ({ message }) => {
    console.error('Appetize client error:', message)
    showEmbedError(message)
})

client.on('sessionError', error => {
    console.error('Appetize session failed:', error)

    reportSessionFailure({
        message: error.message,
        config: client.getConfig()
    })

    showSessionError('We could not start this session. Please try again.')
})
```

Implement `showEmbedError` and `showSessionError` using your application's UI. Do not display stack traces to users.

## Recover known configuration errors

Only use a configuration fallback when you know the failure's cause. For example, your application can offer English after an Android language configuration fails.

```typescript
client.on('sessionError', error => {
    if (error.message.includes('Unable to set language')) {
        showSessionError('This language is unavailable on this device.', {
            retry: async () => {
                await client.setConfig({
                    ...client.getConfig(),
                    language: 'en'
                })

                await client.startSession()
            }
        })
    }
})
```

{% hint style="warning" %}
Do not retry automatically without changing a known failing configuration. This can create a retry loop.
{% endhint %}

Use a generic retry action for failures without a known recovery. Validate configuration values before starting a session when possible. See [Configuration](../javascript-sdk/configuration.md) for supported options.
