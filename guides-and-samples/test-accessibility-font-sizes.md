---
description: >-
  Appetize supports easily testing various font sizes, ensuring compatibility
  across all your supported devices for a seamless user experience.
---

# Test Accessibility Font Sizes

## Overview

Dynamic font size testing is integral to crafting an inclusive and user-friendly app experience. It ensures readability across diverse devices, platforms, and languages.&#x20;

By ensuring all supported font sizes work as expected, you enhance accessibility, maintain cross-platform consistency, and support inclusive design principles, contributing to a seamless and engaging user experience for all.

## Android

Android supports the following font scales to be applied to the session:

| Scale            | Value                 |
| ---------------- | --------------------- |
| <h4>Small</h4>   | 0.85                  |
| <h4>Default</h4> | 1.00                  |
| <h4>Large</h4>   | 1.15                  |
| <h4>Larger</h4>  | 1.30                  |
| <h4>Custom</h4>  | Any Value (e.g. 1.75) |

We can apply a font scale to our app or session by making use of the **adbShellCommand** to execute a `font_scale` change e.g.

{% code title="Applying "Large" Scale" %}
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

| Scale                                     | Value                                      |
| ----------------------------------------- | ------------------------------------------ |
| <h4>Extra Small</h4>                      | `UICTContentSizeCategoryXS`                |
| <h4>Small</h4>                            | `UICTContentSizeCategoryS`                 |
| <h4>Medium</h4>                           | `UICTContentSizeCategoryM`                 |
| <h4>Large</h4>                            | `UICTContentSizeCategoryL`                 |
| <h4>Extra Large</h4>                      | `UICTContentSizeCategoryXL`                |
| <h4>Double Extra Large</h4>               | `UICTContentSizeCategoryXXL`               |
| <h4>Triple Extra Large</h4>               | `UICTContentSizeCategoryXXXL`              |
| <h4>Accessibility Medium</h4>             | `UICTContentSizeCategoryAccessibilityM`    |
| <h4>Accessibility Large</h4>              | `UICTContentSizeCategoryAccessibilityL`    |
| <h4>Accessibility Extra Large</h4>        | `UICTContentSizeCategoryAccessibilityXL`   |
| <h4>Accessibility Double Extra Large</h4> | `UICTContentSizeCategoryAccessibilityXXL`  |
| <h4>Accessibility Triple Extra Large</h4> | `UICTContentSizeCategoryAccessibilityXXXL` |

For the latest up to date list, see their documentation [here](https://developer.apple.com/documentation/uikit/uicontentsizecategory).&#x20;

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
