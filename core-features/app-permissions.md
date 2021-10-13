# App permissions

## Who can run your app

When you upload an app to Appetize.io, you receive a link to view your app. This link includes the app's assigned publicKey, and looks like: `https://appetize.io/app/:publicKey`

This `publicKey` is an unguessable cryptographically generated 26-character string. By default, anybody who has your app's link, i.e. its publicKey, will have permission to run your app. Your app link can be easily shared with whomever you'd like, or [embedded](embed-your-app.md) into your own applications. 

Some customers want to restrict access, so that only authenticated users may run their app. For this purpose, we have a configuration option which can be set at either the app-level or the account-level. For the app-level setting, navigate to your [Dashboard](https://appetize.io/dashboard), then click the "manage" link for your app, and finally configure the option under App Permissions. You may also set account-wide permissions on your [Account](https://appetize.io/account). 

## Other app-related permissions

Configure the permissions below to determine whether you need to be authenticated to the account or simply have the Embed or View link for an app in order to perform the following actions. 

* run: run your app 
* networkProxy: specify a network proxy when running app
* networkIntercept: use Appetize.io's intercepting proxy when running the app
* debugLog: view your app's NSLog or Logcat output 
* adbConnect: debug your app by connecting ADB to the hosted emulator 
* androidPackageManager: allow the installation of additional APK's while your app is running



