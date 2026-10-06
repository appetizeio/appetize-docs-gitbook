---
description: >-
  Start a device with the Appetize CLI, drive the app, and save the screenshot
  and recording that show the check passed.
---

# Test an app with the CLI

The CLI starts a device and drives your app from the terminal. You use it to perform a check and keep the screenshot and recording.

This example uses the [TODO app](https://github.com/appetizeio/todo-app). The same commands work for your own build.

## 1. Install and sign in

Node 22 or later.

```bash
npm install -g @appetize/cli
export APPETIZE_API_TOKEN=tok_xxxxxxxxxxxx
```

Create the token under **Organization → API Tokens**. When your Appetize URL is not `https://appetize.io`, set it too:

```bash
export APPETIZE_ENDPOINT=https://appetize.example.com
```

## 2. Upload the app

```bash
curl -fsSL -o todo-app.apk \
  https://github.com/appetizeio/todo-app/releases/latest/download/todo-app.apk

appetize build upload ./todo-app.apk --wait
```

The command prints an `id`. That is the build id you pass to `session start`. If the app is already uploaded, copy the id from `appetize build list` instead.

## 3. Start a device

```bash
appetize device list --platform android
appetize session start pixel7 YOUR_BUILD_ID --session-id todo
```

Use a device id from the list. `pixel7` is a common one.

You should see the phases end in `ready`, then a `viewerUrl` such as `http://127.0.0.1:52518/`. Open it.

The first launch shows a welcome screen. Dismiss it:

```bash
appetize tap --select-text 'Skip'
```

You should see the TODO list. The title is **Todo**.

## 4. Run the check

This check opens a deep link and confirms the seeded task is on screen.

```bash
mkdir -p demo
appetize open 'todoapp://task/deeplink'
appetize inspect --select-text 'Open a task with a deep link' --pretty
appetize screenshot ./demo/task.png
appetize recording start ./demo/todo
appetize tap --select-text 'All'
appetize recording stop
appetize session stop
```

You should get `demo/task.png` and `demo/todo.mp4`. The screenshot shows the row **Open a task with a deep link**. `inspect` is how you see that text. `tap` and `open` are how you act. The PNG and MP4 are what you keep.

If inspect says the element was not found, run `appetize inspect` with no selector and use the text it prints.

`session stop` releases the device.
