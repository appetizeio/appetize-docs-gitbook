---
description: >-
  Capture user interactions and play them back with ease using Appetize's
  AppRecorder. Test and reuse app workflows (e.g. user login) on different
  devices effortlessly.
---

# UI Automation

## AppRecorder

Users can easily record and replay their interactions with our Appetize Devices using `AppRecorder`. These recordings capture the running application's user interface elements and are designed to handle minor app changes without any issues.&#x20;

You can even record on one device, like an iPhone, and play it back on another device, such as an iPad.

{% hint style="info" %}
We welcome [customer feedback](mailto:hello@appetize.io) as we continue to refine our APIs, and the underlying technology powering our JavaScript SDK.&#x20;
{% endhint %}

### Recording Actions

#### With JavaScript SDK

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

Recorded actions can be serialized as `JSON` and stored so that you can replay them later.

{% code title="Example of a 'click' action" fullWidth="false" %}
```javascript
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
{% endcode %}

### Playing Actions

#### With JavaScript SDK

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

{% hint style="info" %}
See [Playback Event Matching](../javascript-sdk/automation/playback-event-matching.md) for more information on how we match views.
{% endhint %}

## Programmatic Interactions

The device can also be interacted with programmatically through our JavaScript API.

{% content-ref url="../javascript-sdk/automation/device-commands.md" %}
[device-commands.md](../javascript-sdk/automation/device-commands.md)
{% endcontent-ref %}

{% content-ref url="../javascript-sdk/automation/touch-interactions.md" %}
[touch-interactions.md](../javascript-sdk/automation/touch-interactions.md)
{% endcontent-ref %}

## UI Testing with Appetize

We offer a [Playwright](https://playwright.dev/) integration that uses our JavaScript SDK to test your apps.&#x20;

{% content-ref url="../javascript-sdk/playwright/" %}
[playwright](../javascript-sdk/playwright/)
{% endcontent-ref %}
