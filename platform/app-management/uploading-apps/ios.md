---
description: >-
  To get started, Appetize requires a .zip or .tar.gz file containing your
  compressed .app bundle.
---

# iOS

Appetize currently only supports iOS Simulator builds (**.app**). A simulator build can be run in the iOS Simulator with Xcode. AppStore distribution device builds (**.ipa**) are not currently supported.

{% hint style="info" %}
For optimal performance and compatibility, we recommend uploading ARM builds of your iOS app.&#x20;
{% endhint %}

## Finding your .app file

### With Xcode

The easiest way to get the iOS Simulator build is to run and build your application in Xcode while targeting an iOS Simulator

<figure><img src="../../../.gitbook/assets/Screenshot 2023-04-28 at 15.42.41.png" alt=""><figcaption><p>Build and run your application from Xcode while targeting a simulator</p></figcaption></figure>

Once the build is complete and the app is running in the simulator, you can locate the `.app` file by navigating to **Product** -> **Show Build Folder in Finder** -> **Products/Debug-iphonesimulator**

<figure><img src="../../../.gitbook/assets/Screenshot 2023-04-28 at 15.45.53.png" alt="" width="265"><figcaption><p>Show build folder in Xcode</p></figcaption></figure>

### With Xcode Command Line Tools

You can also generate the iOS Simulator build of your app by building it directly via the command line using `xcodebuild`.

#### With .xcodeproj

{% code overflow="wrap" %}
```
xcodebuild -project '{project_name}.xcodeproj' \
 -scheme '{scheme_name}' \
 -sdk iphonesimulator \
 -configuration Debug
```
{% endcode %}

#### With .xcworkspace

{% code overflow="wrap" %}
```
xcodebuild -workspace '{your_workspace_name}.xcworkspace' \
 -scheme '{scheme_name}' \ 
 -sdk iphonesimulator \
 -configuration Debug
```
{% endcode %}

The `app` file can then be found under

```
build/Debug-iphonesimulator/
```

## Compress your .app file

Once you have located your `.app` file, Appetize requires it to be in a compressed `zip` or `tar.gz` file e.g.

```
zip -r {app name}.zip {app name}.app
```

## Troubleshooting

If you are having trouble running your uploaded iOS app in Appetize, we recommend trying to run the same app on an simulator provided by Apple in Xcode.

Once your simulator is launched, you can simply drag over the `app` into the simulator window.

Also check our [Knowledge Base](https://support.appetize.io/) for frequently asked questions and solutions.
