# Overview

The App Recorder is an experimental feature which allows users to record and playback interactions with the app. The recordings are based on the app's user interface elements, and are designed to be robust against small changes in your app. A recording can even be made on one device and played back on another device (e.g. iPhone 6 vs iPhone XS).

The app recorder is disabled by default. To enable, append `&record=true&xdocMsg=true` to your app's url.

We welcome your feedback and bug reports as we continue developing this feature. 

You may see a basic illustrative example at [https://jsfiddle.net/appetize/829fabph/](https://jsfiddle.net/appetize/829fabph/). 

### Known Issues

* Unable to look into the contents of iOS web views
* Performance issues if iOS apps are backgrounded
* iOS picker controls are not well supported
* scrollToElement not yet implemented on iOS

