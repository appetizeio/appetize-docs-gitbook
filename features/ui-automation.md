---
description: >-
  Capture user interactions and play them back with ease using Appetize's
  Automation Recorder. Test and reuse app workflows (e.g. user login) on
  different devices effortlessly.
---

# Automations

## Automation Recorder

Users can easily record and replay their interactions with our Appetize Devices using Appetize's Automation Recorder. These recordings capture the running application's user interface elements and are designed to handle minor app changes without any issues.

You can even record on one device, like an iPhone, and play it back on another device, such as an iPad.

{% hint style="info" %}
We welcome [customer feedback](mailto:hello@appetize.io) as we continue to refine our APIs, and the underlying technology powering our JavaScript SDK.
{% endhint %}

### Recording Actions

#### With App Page

The app page provides an easy way to enable **Automation Recorder** and logging out all of the user actions that took place. You can access this via your app's app link

```
https://appetize.io/app/{appId|buildId|publicKey}
```

or by going to your [Apps](https://appetize.io/apps) page and clicking `Start` on the app you want to inspect.

<figure><img src="../.gitbook/assets/Screenshot 2025-03-21 113458.png" alt=""><figcaption><p>Select <code>Start</code> on your app</p></figcaption></figure>

Once you are on your app page, you can enable **Automation Recorder** by toggling the button to on.

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption><p>Enable Automation Recorder</p></figcaption></figure>

As you interact with the session, **Automation Recorder** will automatically pick up all the actions and log them out in the **Automation Recorder** tab.

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption><p>All actions that took place during the session will be logged in the <strong>Automation Recorder</strong> tab.</p></figcaption></figure>

These actions can then be exported to either JSON for playback later or to a Playwright test file for testing purposes:

<figure><img src="../.gitbook/assets/Screenshot 2025-03-21 114115.png" alt=""><figcaption><p>Export <strong>Automation Recorder</strong> Actions for later playback or for testing.</p></figcaption></figure>

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

{% code title="Example of an action" fullWidth="false" %}
```javascript
{
    type: 'click',
    xPos: 105,
    yPos: 645,    
    element: {
        text: 'Login'       
    }
}
```
{% endcode %}

### Playing Actions

#### With App Page

The app page makes it simple to turn on **AppRecorder** and import a JSON file with past user actions for replay. Just use your app's link to access and get started:

```
https://appetize.io/app/{appId|buildId|publicKey}
```

or by going to your [Apps](https://appetize.io/apps) page and clicking `Start` on the app you want to play the actions on.

<figure><img src="../.gitbook/assets/Screenshot 2025-03-21 113458.png" alt=""><figcaption><p>Select <code>Start</code> on your app</p></figcaption></figure>

Once you are on your app page, you can enable **Automation Recorder** by toggling the button to on.

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption><p>Enable <strong>Automation Recorder</strong></p></figcaption></figure>

To import the JSON file with the user actions to replay, select the "Import JSON" button in the **Automation Recorder** tab and then select "Replay" to start a replay of the user actions that took place.

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption><p>Import your JSON file and select Replay to replay the user actions.</p></figcaption></figure>

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
See [Touch Interactions](../javascript-sdk/automation/touch-interactions.md) for more information on how we match views and some best practices.
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

We offer a [Playwright](https://playwright.dev/) integration that uses our JavaScript SDK to test your apps.

{% content-ref url="../testing/" %}
[testing](../testing/)
{% endcontent-ref %}
