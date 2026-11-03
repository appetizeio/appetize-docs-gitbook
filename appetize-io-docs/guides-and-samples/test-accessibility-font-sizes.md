---
description: >-
  Appetize supports easily testing various font sizes, ensuring compatibility
  across all your supported devices for a seamless user experience.
---

# Test Accessibility Font Sizes

## Overview

Dynamic font size testing is integral to crafting an inclusive and user-friendly app experience. It ensures readability across diverse devices, platforms, and languages.

By ensuring all supported font sizes work as expected, you enhance accessibility, maintain cross-platform consistency, and support inclusive design principles, contributing to a seamless and engaging user experience for all.

## Android

Android supports the following font scales to be applied to the session:

| Scale       | Value                 |
| ----------- | --------------------- |
| **Small**   | 0.85                  |
| **Default** | 1.00                  |
| **Large**   | 1.15                  |
| **Larger**  | 1.30                  |
| **Custom**  | Any Value (e.g. 1.75) |

We can apply a font scale to our app or session by making use of the **adbShellCommand** to execute a `font_scale` change e.g.

{% code title="Applying " %}
```sh
settings put system font_scale 1.15
```
{% endcode %}

{% tabs %}
{% tab title="Query Parameter" %}
<pre class="language-url"><code class="lang-url"><strong>&#x26;adbShellCommand=settings+put+system+font_scale+1.15
</strong></code></pre>
{% endtab %}

{% tab title="JavaScript SDK" %}
{% code overflow="wrap" %}
```typescript
await session.adbShellCommand("settings put system font_scale 1.15")
```
{% endcode %}
{% endtab %}
{% endtabs %}

## iOS

iOS supports the following dynamic font scales to be applied to the session:

| Scale                                | Value                                      |
| ------------------------------------ | ------------------------------------------ |
| **Extra Small**                      | `UICTContentSizeCategoryXS`                |
| **Small**                            | `UICTContentSizeCategoryS`                 |
| **Medium**                           | `UICTContentSizeCategoryM`                 |
| **Large**                            | `UICTContentSizeCategoryL`                 |
| **Extra Large**                      | `UICTContentSizeCategoryXL`                |
| **Double Extra Large**               | `UICTContentSizeCategoryXXL`               |
| **Triple Extra Large**               | `UICTContentSizeCategoryXXXL`              |
| **Accessibility Medium**             | `UICTContentSizeCategoryAccessibilityM`    |
| **Accessibility Large**              | `UICTContentSizeCategoryAccessibilityL`    |
| **Accessibility Extra Large**        | `UICTContentSizeCategoryAccessibilityXL`   |
| **Accessibility Double Extra Large** | `UICTContentSizeCategoryAccessibilityXXL`  |
| **Accessibility Triple Extra Large** | `UICTContentSizeCategoryAccessibilityXXXL` |

For the latest up to date list, see their documentation [here](https://developer.apple.com/documentation/uikit/uicontentsizecategory).

We can apply the initial dynamic font scale by sending the content size category value as a launch argument to our session when launched e.g.

{% code title="Apply Double Extra Large Dynamic Font Scale" %}
```swift
[ "-UIPreferredContentSizeCategoryName", "UICTContentSizeCategoryXXL" ]
```
{% endcode %}

{% tabs %}
{% tab title="Query Parameter" %}
{% code overflow="wrap" %}
```url
&launchArgs=%5B+"-UIPreferredContentSizeCategoryName"%2C+"UICTContentSizeCategoryXXL"+%5D
```
{% endcode %}
{% endtab %}

{% tab title="JavaScript SDK" %}
```typescript
const session = await client.startSession({
    ...
    launchArgs: [ "-UIPreferredContentSizeCategoryName", "UICTContentSizeCategoryXXL" ]
})
```
{% endtab %}
{% endtabs %}
