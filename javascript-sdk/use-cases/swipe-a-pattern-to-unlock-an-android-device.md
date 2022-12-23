# Swipe a pattern to unlock an Android device

```javascript
const session = await client.startSession()

// Swipe in a square pattern starting at the given element
await session.swipe(
   new window.appetize.SwipeGesture()
    .from({
       'resource-id': 'passcode_unlock'
    })
    .to(0, 100)
    .to(40, 100)
    .to(40, 200)
    .to(0, 200)
    .to(0, 100)
)
```
