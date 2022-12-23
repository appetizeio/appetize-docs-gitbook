# Recording and playback

User interactions can be recorded and played back again either on the same session or a later one. The recordings are based on the app's user interface elements, and are designed to be robust against small changes in your app. A recording can even be made on one device and played back on another device (e.g. iPhone 6 vs iPhone XS).

## Recording Actions

When the user interacts with the device, the session will emit an `action` event:

```javascript
const session = await client.startSession()

let actions = []
session.on('action', action => {
    actions.push(action)
})

// later on, replay them
await session.playActions(Actions)
```

Recorded actions can be serialized as JSON and stored so that you can replay them later.&#x20;

```javascript
// example of a 'click' action
{
    type: 'click',
    xPos: 105,
    yPos: 645,    
    element: {
        text: 'Login',
        class: 'UIView',
        baseClass: 'UIResponder',        
    }
}
```

## Playing Actions

You can play an action on the device using `session.playAction`

```javascript
await session.playAction({
   type: 'click',
   element: {
      text: "submit",
      accessibilityIdentifier: "submit_button",
      class: "UIView"
   }
})
```

Multiple actions can be played back using `session.playActions`

```javascript
await session.playActions([
   {
      type: 'type',
      element: {
         accessibilityIdentifier: "email_field",
      }
   },
   {
      type: 'click',
      element: {
         text: "submit"
      }   
   }
])
```
