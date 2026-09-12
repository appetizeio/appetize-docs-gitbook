# Session Defaults

Every Appetize session starts from a set of defaults — device, language, timeouts, developer tools. Session Defaults sets those once for the whole organization, instead of repeating them in every link, embed and SDK call.

It lives under **Organization → Session Defaults** at [appetize.io/organization/session-defaults](https://appetize.io/organization/session-defaults). Admins only.

![](https://2147444700-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-MJUveBCJfn0GR8-hlqi%2Fuploads%2FECANKmtEJSkryubfOGAT%2Fsession-defaults-sections.png?alt=media\&token=2c6f897f-ea7a-4544-b9de-bfd4b9de2f32)

## What's on the page

Twenty-eight settings in five sections:

| Section                      | Covers                                                             |
| ---------------------------- | ------------------------------------------------------------------ |
| **Session Behavior**         | How long a session lasts, and what happens when it starts and ends |
| **Default Devices**          | The iOS and Android device and OS version a session opens on       |
| **Location and language**    | Language, locale, timezone, mock location, iOS keyboard            |
| **Display and presentation** | Scale, orientation, appearance, device frame                       |
| **Developer tools**          | Debug logs, ADB, intercept proxy, audio, automation recorder       |

Each one is the account-level default for a value you can already set per session, so every setting is documented where that per-session value is. [JavaScript SDK configuration](https://docs.appetize.io/javascript-sdk/configuration) is the complete reference; [Query Params Reference](https://docs.appetize.io/platform/query-params-reference) covers the same settings as URL parameters. Several also have their own page — [Devices & OS Versions](https://docs.appetize.io/features/devices-and-os-versions), [Language and Locale](https://docs.appetize.io/features/language-and-locale), [Mock Location](https://docs.appetize.io/features/mock-location), [ADB tunnel](https://docs.appetize.io/features/advanced-features/android/adb-tunnel), [Debug logs](https://docs.appetize.io/features/debug-logs).

Use the search box rather than scrolling. It matches names, descriptions and platform tags across all five sections.

![](https://2147444700-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-MJUveBCJfn0GR8-hlqi%2Fuploads%2F29ayuhQFoPtUQEmvIW4y%2Fsession-defaults-search.png?alt=media\&token=76c2493e-64a4-4460-ae6d-d0d6fa175ad6)

## How a value is chosen

**Session time limit** and **Inactivity timeout** are enforced by Appetize, so they apply to every session however it started — app link, embed, JavaScript SDK, CLI or REST API — and no query parameter overrides them. The first value set wins:

1. The app build's own setting (Apps → your app → the build → Settings)
2. Your session default
3. Appetize's default — no time limit, 2 minute inactivity timeout

Every other setting is the session's starting configuration, so a per-session value wins over your default: `?device=pixel7&language=fr` still does what it says.

1. The query parameter, or `config` passed to the JavaScript SDK
2. Your session default
3. Appetize's default

## Changing a setting

![](https://2147444700-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-MJUveBCJfn0GR8-hlqi%2Fuploads%2FI7ozQno1Cwa7IgmqHYYk%2Fsession-defaults-behavior.png?alt=media\&token=73c72cf3-3a31-4c92-9a3e-f911c5447b22)

**Default (…)** means you have not set anything, and the value in brackets is what Appetize uses. Changes save as you make them — there is no save button — and each section header counts how many of its settings you have changed.

Picking **Default** again clears the stored value rather than pinning it, so you keep following Appetize's default if it changes later.

* **Session time limit** — Unlimited, or 5 minutes to 8 hours.
* **Inactivity timeout** — 30 seconds to 2 hours. See [Session Inactivity Timeout](https://docs.appetize.io/platform/session-inactivity-timeout) for per-build timeouts.
* **Device and OS version** save as a pair, so you cannot store a combination that would fail to start.

{% hint style="info" %}
Defaults apply to sessions started from now on. A session that is already running is not affected.
{% endhint %}

The **Permissions (Legacy)** switches at the bottom of the page are covered in [App Permissions](https://docs.appetize.io/platform/app-management/app-permissions).
