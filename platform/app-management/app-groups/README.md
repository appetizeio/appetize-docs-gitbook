# App Groups

An **App Group** is a named set of apps that Appetize installs together on the same device, in one session.

Normally a session runs one build. A group runs up to ten, side by side on the same device, sharing the same state — so the apps can hand off to each other as they would on a real phone.

### When to use one

* **A companion app alongside the app under test.** A small internal app that mints a token, seeds data or switches environment, next to the real app. This is the usual way to do [impersonation](https://docs.appetize.io/guides-and-samples/impersonation) without building the feature into your production app.
* **App-to-app flows.** Deep links, OAuth handoffs, share sheets, "open in" — anything where the interesting behaviour is one app calling another.
* **A suite in one demo.** Several products from the same family on one device, so a prospect or a new hire can move between them without restarting a session.
* **A main app plus a debug tool.** A log viewer, a mock server UI or a QA harness that has to be on the device with the app, not beside it in a browser tab.

If your apps never talk to each other, you do not need a group — run separate sessions.

### How a group works

A group stores a **query per app** rather than a fixed list of builds: an app, and optionally which build of it. Appetize resolves those queries each time a session starts, so a group left on **Latest Build** keeps picking up new uploads without anyone editing it.

Four things follow from that:

* A group is **one platform**, fixed when you create it. Cover both platforms with two groups.
* Sessions **take longer to start**, because every app is installed first.
* If a query stops matching, that app is **skipped and the session still starts** without it.
* The session timeout is the **longest** timeout among the group's builds.

### What launches

{% hint style="warning" %}
A group of **two or more** apps does not launch anything. The session opens on the device home screen with every app installed, and you tap in — or tell Appetize what to launch.
{% endhint %}

This surprises people, because a group holding a **single** app does auto-launch it. Set [`launchApp`](https://docs.appetize.io/platform/query-params-reference) to pick a starting app:

```
https://appetize.io/embed/ag_...?device=pixel7&launchApp=com.example.myapp
```

`launchApp` takes an app id; on Android it also accepts `packageName/activityName`. `launchApp=false` suppresses launching entirely. From the [JavaScript SDK](https://docs.appetize.io/javascript-sdk) you can also launch at any point during the session with `session.launchApp('com.example.myapp')`.

### Deep links into a group

On **iOS**, a `launchUrl` is opened once the session is up and the OS picks the app that handles it. This is the case groups are best at.

On **Android**, a `launchUrl` goes to whichever app finished installing first, which is not necessarily the first app in your group. Pin it by passing `launchApp` alongside the URL.

### Using a group

A group has an id of the form `ag_…`, shown as **Group ID** on the group's page. It works anywhere a build id works — an app link, an [embed](https://docs.appetize.io/platform/embedding-apps), a [share link](https://docs.appetize.io/platform/sharing-apps), the [JavaScript SDK](https://docs.appetize.io/javascript-sdk) `buildId`, and the CLI:

```bash
appetize session start pixel7 ag_...
```

Groups are created and edited in the dashboard or through the **v2 API** (`/v2/app-groups`); the v1 API can read a group but not change one.

### Limits

| Limit               | Value                |
| ------------------- | -------------------- |
| Apps per group      | 10                   |
| Platforms per group | 1, fixed at creation |
| Group name          | 50 characters        |

Launch arguments, launch params and auto-granted permissions are **session-wide**, not per app — they apply to the app that gets launched.

### Next steps

* [Creating a group](https://docs.appetize.io/platform/app-management/app-groups/creating-a-group) — build it and choose which build each app uses
