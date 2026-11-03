---
description: Open a DeepLink and ensure analytics API calls happen
---

# Validate Analytics Events

```javascript
const session = await client.startSession({ 
    proxy: 'intercept', // receive network requests made by device
    debug: true         // receive debug messages from device
})

// check network requests
session.on('network', (data) => {
    // intercepted network request
    if (data.type === 'request') {
        console.log(`[${data.request.method}]: ${data.request.url}`)
    } 
    
    // intercepted network response
    if (data.type === 'response' && data.request.method === 'POST') {
        console.log(data.response.postData)
    }
})

// check debug logs
session.on('log', (data) => {
    console.log(data.message)
})

await session.openUrl('scheme://example.com/deep-link-url')
```
