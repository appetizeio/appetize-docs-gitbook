# Overview

You may use our API to upload new apps, update existing apps, change app settings, and list apps under your account.

To upload an iOS app, you must first create a Simulator build. Compress your `.app` folder into a `.zip` or `.tar.gz` file. Then upload it to a publicly accessible web server where we can download and process it. Alternatively, call our API using the [direct upload](https://appetize.io/#direct-uploads) method.

Similarly for Android, upload your app's `.apk` package to a publicly accessible web server or use the [direct upload](https://appetize.io/#direct-uploads) method.

When uploading a new app, a successful upload \(response code in the 200's\) will return JSON containing your new app's publicKey, which identifies your app. Save this identifier for future use.

