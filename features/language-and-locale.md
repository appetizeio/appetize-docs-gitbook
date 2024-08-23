---
description: >-
  Appetize supports multiple languages and locales for running your mobile apps
  in different regions and languages.
---

# Language & Locale

## Language

{% hint style="warning" %}
Note that for `iOS` we currently only set the language at the app level. Our Private Cloud offerings allow for setting system level language configurations. [Contact us](https://appetize.io/contact-us) to learn more.
{% endhint %}

### With Query Parameter

Set the language of the device by adding the `language` query parameter to your app or embed URL.

```uri
&language=af_ZA
```

See [Query Params Reference](../platform/query-params-reference.md#language) for more information.

### With JavaScript SDK

Set the language of the device via our JavaScript SDK

#### With Configuration

```typescript
await client.setConfig({
    language: 'af_ZA',
    ...
})
```

See [Configuration](../javascript-sdk/configuration.md#language) for more information.

#### With `SetLanguage`

```typescript
await session.setLanguage("af_ZA")
```

See [API Reference](../javascript-sdk/api-reference.md#setlanguage) for more information

## Locale

_iOS Only_

### **With Query Parameter**

Set the locale of the device by adding the `locale` query parameter to your app or embed URL.

```
&locale=fr_FR
```

See [Query Params Reference](../platform/query-params-reference.md#locale) for more information

### **With JavaScript SDK Configuration**

Set the locale of the device via our JavaScript SDK configuration

```typescript
await client.setConfig({
    locale: 'fr_FR',
    ...
})
```

See [Configuration](../javascript-sdk/configuration.md#locale) for more information

## Timezone

_Android Only_

### **With Query Parameter**

Set the time zone of the device by adding the `timezone` query parameter to your app or embed URL.

```
&timezone=Australia%2FAdelaide
```

See [Query Params Reference](../platform/query-params-reference.md#timezone) for more information

### **With JavaScript SDK Configuration**

Set the time zone of the device via our JavaScript SDK configuration

```typescript
await client.setConfig({
    timezone: 'Australia/Adelaide',
    ...
})
```

See [Configuration](../javascript-sdk/configuration.md#timezone) for more information

## iOSKeyboard

_iOS Only_

We also support an `iosKeyboard` [Query Parameter](language-and-locale.md#with-query-parameter-3) and [JavaScript SDK Configuration](language-and-locale.md#with-javascript-sdk-configuration-2) to specify the exact keyboard for iOS. The Android keyboard does not need this feature, as it updates automatically based on the language specified. A full list of supported keyboards can be found [here](https://pgssoft.github.io/AutoMate/Enums/SoftwareKeyboard.html).

### **With Query Parameter**

Set the keyboard of the device by adding the `iosKeyboard` query parameter to your app or embed URL.

```
&iosKeyboard=ja_JP@sw
```

See [Query Params Reference](../platform/query-params-reference.md#ioskeyboard) for more information

### **With JavaScript SDK Configuration**

Set the time zone of the device via our JavaScript SDK configuration

```typescript
await client.setConfig({
    iosKeyboard: 'ja_JP@sw',
    ...
})
```

See [Configuration](../javascript-sdk/configuration.md#ioskeyboard) for more information.

## Sample Usage

#### Japanese language and keyboard

[https://appetize.io/demo?language=ja\&iosKeyboard=ja\_JP@sw](https://appetize.io/demo?language=ja\&iosKeyboard=ja\_JP@sw)

#### French language with French AZERTY keyboard

[https://appetize.io/demo?language=fr\&iosKeyboard=fr\_FR@sw](https://appetize.io/demo?language=fr\&iosKeyboard=fr\_FR@sw)
