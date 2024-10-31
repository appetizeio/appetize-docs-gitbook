---
description: >-
  Automate mobile app screenshots effortlessly using Appetize - Save time on
  releases, better quality assurance, improved customer support and more!
---

# Screenshot Automation

## Overview

Screenshot automation refers to the process of automatically capturing screenshots of your application's screens without any manual interaction required from a user.

Screenshot automation can serve various purposes, including:

* [**Testing and Quality Assurance**](screenshot-automation.md#testing-and-quality-assurance)
* [**Apple AppStore and Google PlayStore Submissions**](screenshot-automation.md#apple-appstore-and-google-playstore-submissions)
* [**Compliance and Customer Support**](screenshot-automation.md#compliance-and-customer-support)
* **Reporting and Documentation**
* **User Experience Research and A/B Testing**

## Testing and Quality Assurance

Automated screenshots can be used to verify the visual appearance and layout of an application under different scenarios (e.g. different languages, locales, orientations, device types etc.)

By making use of Playwright, you can write [Visual Comparison](https://playwright.dev/docs/test-snapshots) (Snapshot) tests to verify that screens are rendered as expected whenever a new build/pull request (or other condition) occurs.

For more information see [Screenshot Comparisons](https://docs.appetize.io/javascript-sdk/playwright/writing-tests#screenshot-comparisons) under our [Writing Tests](../testing/writing-tests.md) article.

{% hint style="info" %}
For clients who prefer manually reviewing the generated screenshots, Playwright generates files for all requested screenshots in the output folder. Alternatively, you can follow a process similar to [App store submissions](screenshot-automation.md#apple-appstore-and-google-playstore-submissions) to generate and save screenshots without requiring a Playwright setup.
{% endhint %}

## Apple AppStore and Google PlayStore Submissions

Both Apple and Google (and other App stores) have specific requirements for screenshot submissions that includes submitting compelling images that accurately represent the app's features.

Screenshot automation offers substantial advantages in this context. By automating the screenshot capture process, developers can automatically generate the required images for all their app features on all the supported device types and in the correct locale and language.

To get started:

### 1. Gather the requirements of the screenshots

* Determine the key **features** that you would like to capture in your screenshots
* If the app supports multiple **languages** and **locales**, plan for localised screenshots to cater to the different regions/stores.
* Decide on the specific **device types** and **screen sizes** you want to capture screenshots for. See [PlayStore Screenshot guidelines](https://support.google.com/googleplay/android-developer/answer/9866151?hl=en) and [AppStore Screenshot guidelines](https://developer.apple.com/help/app-store-connect/reference/screenshot-specifications/) for assistance on recommended device types.
* Consider capturing screenshots in both portrait and/or landscape **orientations**, depending on the app's responsive design.

### 2. Set up our Javascript SDK

In order to take screenshots of the device session, you will need to make use of our Javascript SDK. See our [Getting Started](../javascript-sdk/) page for more info on how to get that set up.

### 3. Build out an object/structure that would match your requirements

For illustrative purposes, lets imagine the following requirements:

* 1 iOS App
  * 7 devices (e.g. iPhone 14 Pro on iOS 16, iPhone 12 on iOS 15 etc.)
  * 4 Features/Screens
  * 3 Languages (English, German and French)
* 1 Android App
  * 7 Devices (e.g. Pixel 7 on Android 13, Galaxy Tab S7 on Android 12)
  * 4 Features/Screens
  * 3 Languages (English, German and French)

A structure matching those requirements could look like this:

```javascript
const config = {
    /***
     * The apps to generate screenshots for.
     */
    apps: [
        {
            name: "{Name of App 1}",
            publicKey: "{publicKey of App 1}",

            /**
             * The devices to generate screenshots for.
             */
            devices: [
                {
                    displayName: "iPhone 14 Pro",
                    device: "iphone14pro",
                    osVersion: "16.2",
                },
                {
                    displayName: "iPhone 12",
                    device: "iphone12",
                    osVersion: "15",
                }
                // and more devices ...
            ],
            /**
             * The languages to generate screenshots for.
             */
            languages: [
                "en", "fr", "de" // and more languages ...
            ],

            /**
             * The screens/features to generate screenshots for. Each screen will be navigated to and a screenshot will be taken.
             * Assume that the app might already be launched and that you need to re-navigate to the screen.
             */
            screens: [
                {
                    displayName: "{display name of the screen/feature 1}",
                    playbackActions: async (client, session, language) => {
                        // Steps to navigate to screen ( we will expand on this below) ...
                    }
                },
                {
                    displayName: "{display name of the screen/feature 2}",
                    playbackActions: async (client, session, language) => {
                     // Steps to navigate to screen ( we will expand on this below) ...
                    }
                } // and more screens.
            ]
        },
        // and more apps ...
    ],
};
```

### 4. Navigate to appropriate screen/feature

In the above structure, we've defined an asynchronous function called `playbackActions` that we can call to navigate to a particular screen/feature in our app.

{% hint style="info" %}
We recommend treating each `playbackActions` function as independent from another for better consistency e.g. if you provide permissions in a previous function, do not assume it will be available in the next function.
{% endhint %}

To define the steps to navigate to the particular screen, you can make use of all our automation functions available in our Javascript SDK. See [Touch interactions](../javascript-sdk/automation/touch-interactions.md) and [API Reference](../javascript-sdk/api-reference/) for more information. A sample screen navigation could look like this:

```javascript
async function playbackActions(client, session. language) {
   await session.findElement({
      attributes: {
          'resource-id': "com.sampleapp:id/nav_tab_homepage"
      }
   });
   await session.tap({
      attributes: {
          'resource-id': "com.sampleapp:id/nav_tab_homepage"
      }
   });
   await session.findElement({
      attributes: {
          'resource-id': "com.sampleapp:id/homepage_first_card"
      }
   });
}
```

### 5. Putting it all together

Now that we have all the configurations and steps needed to take all the screenshots required, lets put it all together by iterating over each of them:

{% hint style="info" %}
Consider updating the existing session instead of starting a new session whenever possible e.g. use `setLanguage()` instead of setting a new configuration with `startSession/setConfig()`
{% endhint %}

```javascript
// iterate over every app.
for (const app of config.apps) {

    // iterate over every device
    for (const device of app.devices) {
        
        // start a new Session matching the app and device
        const sessionConfig = {
            publicKey: app.publicKey,
            device: device.device,
            osVersion: device.osVersion,
            // ... other configurations
        }
        const session = await client.startSession(sessionConfig);
    
        // iterate over each language 
        for (const language of app.languages) {
        
            // set Language 
            await session.setLanguage(language);
            
            // iterate over each feature/screen
            for (const screen of app.screens) {
                await screen.playbackActions(client, session, language);
                
                 // Take and upload the screenshot remotely
                const screenshot = await session.screenshot();
                await uploadSomewhere(screenshot.data, screenshot.mimeType);
        
                // OR take screenshot and store it in memory to download it later locally
                const screenshot = await session.screenshot('base64');
                imageData.push({
                    data: screenshot.data,
                    mimeType: screenshot.mimeType,
                    action: action
                });
            }
        }
    }
}
```

{% hint style="info" %}
For a complete example of this scenario and how to download these images locally, have a look at our [Screenshot Automation](https://github.com/appetizeio/appetize-samples/tree/main/screenshot\_automation) sample in our [Samples Repository](https://samples.appetize.io/).
{% endhint %}

## Compliance and Customer Support

There are several scenarios where you might want a step by step screenshot of actions taken by the user interacting with the Appetize session e.g.

* Support agents can use screenshot automation to provide step-by-step visual instructions to customers. When guiding users on how to perform specific tasks or resolve issues, a series of annotated screenshots can be incredibly helpful and user-friendly.
* For compliance purposes you might want screenshots of all actions taken

With Appetize, you could automate generating of a screenshot on every step the user takes.

### 1. Set up our Javascript SDK and start a session

In order to take screenshots of the device session, you will need to make use of our Javascript SDK. See our [Getting Started](../javascript-sdk/) page for more info on how to get that set up.

```typescript
const session = await client.startSession()
```

### 2. Listen to all customer support interactions with the Appetize session

```typescript
session.on('action', action => {
   // a user interaction took place so take a screenshot
   await takeScreenshot(action);
})
```

### 3. Take a screenshot and keep it locally or remotely

{% code fullWidth="false" %}
```javascript
async function takeScreenshot(action) {
    // upload the screenshot remotely
    const screenshot = await session.screenshot();
    await uploadSomewhere(screenshot.data, screenshot.mimeType);
    
    // OR store it in memory to download it later locally
    const screenshot = await session.screenshot('base64');
    imageData.push({
        data: screenshot.data,
        mimeType: screenshot.mimeType,
        action: action
    });
}
```
{% endcode %}

{% hint style="info" %}
For a more complete example on how to store the screenshots locally for download, see our [Screenshot Automation Sample Repository](https://github.com/appetizeio/appetize-samples/tree/main/screenshot\_automation).
{% endhint %}
