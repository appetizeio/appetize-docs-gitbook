---
description: Migrating to the New Appetize Automation Engine (iOS 26 and Beyond)
---

# Automation Engine - Migration Guide

We’re excited to introduce our **new automation engine**, launching first with **iOS 26**.\
This update brings improved **stability**, **stronger integration with Appetize**, and full support for **modern frameworks** like **SwiftUI**, **Flutter**, **Compose Multi-Platform,** **React Native** and more.&#x20;

It’s largely **backward-compatible with existing automation flows**, so in most cases your existing **JS SDK commands will continue to work without changes**.

{% hint style="warning" %}
The new engine will reach **all iOS versions within about one month**, after which the old engine will be retired.

Android will follow later, with minimal migration expected.
{% endhint %}

***

## :sparkles: What’s New

### Better Integration Across Appetize

This engine is more tightly integrated with Appetize services, giving us a consistent foundation for all automation features.\
It also makes it easier for us to add new commands, selectors, and advanced testing capabilities in the future.

### Declarative UI Framework Support

Apps built with frameworks such as **SwiftUI**, **Jetpack Compose**, **Flutter and more** are now fully supported.\
In older versions, these apps often appeared as a single, non-interactive surface. The new engine correctly exposes their underlying UI structure, allowing tests to target and interact with individual elements.

### More Stability and Resilience

The new engine is **more forgiving of small UI changes** and **handles variations in layout or timing more smoothly**.

### Regex Support

You can now use **regular expressions** in text selectors for flexible matching.\
This is helpful when text values change dynamically, such as in localized or data-driven UI.

***

## :dart:  Main Areas to Focus On

Most existing automations will continue to work, but there are a few key areas to review when testing on iOS 26.

### 1. Remove UIKit-Specific Selector

The new engine continues to support **accessibility-based selectors** - the same pattern many teams already use - but now makes this the **recommended and primary approach**.

{% hint style="info" %}
Prefer using **accessibility elements** such as labels, identifiers, or visible text.\
They’re stable across app frameworks and align with how modern apps expose their UI.
{% endhint %}

In previous versions, the engine also exposed some UIKit-specific attributes (`class`, `baseClass`, `isHidden`). These are no longer available. If your tests relied on them, you should update to use accessibility identifiers or text instead.

See our[ Selectors Reference](touch-interactions.md#targeting-elements) for guidance and examples.

***

### 2. Text Resolution Changes

If an element has both a `text` value and an `accessibilityLabel`, the label will now **override** the text.\
If `text` is empty, the engine falls back to `accessibilityText`.

```swift
TextField("placeholder", text: $value)
  .accessibilityLabel("My new placeholder text")
// Result: text == "My new placeholder text"

```

{% hint style="info" %}
To capture the raw value instead of the accessibility label, use\
`accessibilityValue` or `accessibilityTitle`.
{% endhint %}

***

### 3. Visibility Semantics

Elements that are off-screen but rendered (e.g., in a `UIStackView` outside the viewport)\
are **no longer reported as interactable**. Scroll to bring them into view before interacting.

{% code title="Scroll first, then tap" %}
```js
await session.swipe({ gesture: 'up', duration: 600 });
await session.tap({
  element: { attributes: { text: 'Past Articles' } }
});
```
{% endcode %}

***

### 4. WebView Selectors

* `id` attributes are not currently exposed for WebViews.
* Use **ARIA** attributes (like `aria-label`) or visible text content instead.

{% code title="Example WebView content" %}
```html
<button role="button" aria-label="Continue checkout">Checkout</button>
```
{% endcode %}

{% code title="Test targeting by visible text" %}
```js
await session.tap({
  element: { attributes: { text: 'Continue checkout' } }
});
```
{% endcode %}

***

### 5. Timeouts

Timeouts are now **best-effort** rather than exact.\
If a check is already in progress, a 1 s timeout may complete slightly later.

```js
await session.waitForAnimations({ timeout: 1000 }); // may finish ~1.5 s
```

***

### 6. `getUI` Response Change

The `getUI` response is now simplified to focus on **what’s visible to the user**.

Previously, it returned both the running app **and** the **Springboard** (system) hierarchies.\
Now, you’ll still see the same top-level structure for compatibility, but only the **first app node** contains content.\
Springboard will be present but empty.

{% tabs %}
{% tab title="Before" %}
App and system content were separated into two distinct sections.

```json
[
  {
    "type": "app",
    "appId": {running app},
    "children": [ ... ] // Your app content
  },
  {
    "type": "app",
    "appId": "com.apple.springboard",
    "children": [ ... ] // Springboard (system UI) content
  }
]
```
{% endtab %}

{% tab title="After" %}
A single combined hierarchy is returned, representing what’s actually visible to the user.

```json
[
  {
    "type": "app",
    "appId": {possible appId},
    "children": [ ... ] // All visible content on screen (e.g. Springboard related content too)
  }
]
```
{% endtab %}
{% endtabs %}

This structure makes the UI tree easier to reason about and aligns with what appears on screen.

***

## ⚠️ Known Issues

### Landscape Automations

Automations running in **landscape orientation currently do not work** with the new engine.\
We are actively working on a fix and expect to resolve this **before the full iOS rollout**.

### **In-App Browser Elements (iOS 26)**

On iOS 26, elements opened inside an **in-app browser** (for example, a web view launched from within your app for login or external content) are currently **not accessible to automation**.

***

## 🗓️ Rollout Timeline

| Phase        | Platform         | Status                               |
| ------------ | ---------------- | ------------------------------------ |
| ✅ Now        | iOS 26           | New engine live                      |
| 🔜 \~1 month | All iOS versions | Full iOS rollout, old engine retired |
| 📅 Later     | Android          | Planned rollout                      |

***

## 💬 Feedback

This rollout marks a major step toward **stable, integrated, and cross-platform automation** within Appetize. If you encounter any unexpected behaviors or migration challenges, please [reach out to us](mailto:hello@appetize.io). Your feedback helps us continue improving and expanding what’s possible with Appetize automations.
