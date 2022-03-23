# Playback options

App links, such as [https://appetize.io/app/\<publicKey>?device=pixel4\&language=en](https://appetize.io/app/%3CpublicKey%3E?device=pixel4\&language=en) can contain many optional query parameters.

You may see these query parameters in action when you run our [online demo](https://appetize.io/demo), and observe changes to your browser's address bar.

These parameters specify:

* `device` - eg. iphone8, iphone11pro, iphone11promax, ipadair2, pixel4, pixel4xl, galaxytabs7
* `osVersion` - the operating system version on which to run your app, e.g. 11.4, 12.2, 13.3, 14.0 _Note: We recommend do not include osVersion as a query parameter when embedding your app, that way will always use our latest default._
* `scale` - values between 10 and 100
* `autoplay` - true or false, default is false. When true, start streaming app on page load.
* `orientation` - portrait or landscape
* `centered` - "vertical", "horizontal" or "both". Centers the device (only when embedding)
* `deviceColor` - black or white
* `screenOnly` - true or false, default is false. When true, only show the screen, i.e. no device frame.
* `xdocMsg` - true or false, default is false. When true, enables [cross-document messages](cross-document-messages.md).
* `language` - [ISO 639-1 & BCP 47](https://stackoverflow.com/questions/7973023/what-is-the-list-of-supported-languages-locales-on-android) language code
* `locale` - Locale ID, eg. en\_GB, fr\_FR (iOS only)
* `iosKeyboard` - iOS software keyboard, eg. iosKeyboard=ja\_JP@sw [available values](https://pgssoft.github.io/AutoMate/Enums/SoftwareKeyboard.html)
* `disableVirtualKeyboard` - (Android only) true or false, default is false. When true, disables the on-screen keyboard.
* `location` - latitude, longitude, eg. 39.903924,116.391432 (Android only)
* `timezone` - specify URL-encoded timezone, eg. Australia%2FAdelaide, [available values](https://en.wikipedia.org/wiki/List\_of\_tz\_database\_time\_zones) (Android only)
* `grantPermissions` - true or false - automatically grant all required app permissions (Android only)
* `hidePasswords` - true or false - hide password visibility when typing (Android only)
* `launchUrl` - specify a deep link to open when your app is launched
* `launchArgs` - specify a url-encoded JSON array of strings to pass when launching your app (iOS only)
* `debug` - true or false, default is false. When true you can view the debug log for your app.&#x20;
* `proxy` - specify a proxy server to route network traffic. e.g. `http://example.com:8080`. For Appetize.io's intercepting proxy, use `proxy=intercept`
* `enableAdb` - true or false. on session start, generate an SSH tunnel to allow ADB connections to the emulator
* `androidPackageManager` - true or false, default is false. Allows installation of additional APKs after app launch
* `appearance` - set to `dark` to set dark mode UI on iOS 13+ and Android 10+
* `params` - a URL-encoded JSON object. This data will be passed to your app on launch. eg. `&params={"foo":"bar"}` which gets URL encoded to `&params=%7B%22foo%22%3A%22bar%22%7D`

The `params` JSON dictionary allows you to pass values to your app on launch. It can be useful to load custom content, skip onboarding, auto-login the specified user, or custom tracking.

To read the values in your iOS app, call `[[NSUserDefaults standardUserDefaults] objectForKey:@"key"]`.

On Android, they will be passed as extras into the intent that launches your app, accessible by calling `getIntent().getStringExtra("key")`, `getBooleanExtra("key")`, etc.

They can also be retrieved from SharedPreferences named "prefs.db", e.g. `getApplicationContext().getSharedPreferences("prefs.db", 0).getString("key", null)`

For convenience, we set the key `"isAppetize": true` when streaming apps. You can detect if your app is running in Appetize.io by calling:

* iOS: `[[NSUserDefaults standardUserDefaults] objectForKey:@"isAppetize"]`
* Android: either of the following methods
  * `getIntent().getBooleanExtra("isAppetize", false)`
  * `getApplicationContext().getSharedPreferences("prefs.db", 0).getBoolean("isAppetize", false)`
