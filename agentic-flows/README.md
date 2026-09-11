---
description: >-
  Run and test mobile apps with AI coding agents — artificial intelligence
  workflows powered by the appetize CLI and its agent skill.
hidden: true
icon: terminal
---

# Agentic Flows

Give an AI coding agent the Appetize CLI and let it drive your app.

The `appetize` CLI runs your iOS or Android app on an Appetize device and drives it from your terminal. Sessions are headless — no browser, no embed — so the same commands work on your machine and in CI.

{% hint style="warning" icon="triangle-exclamation" %}
**Beta.** Command names, flags and output are all still changing between releases.
{% endhint %}

```bash
npm install -g @appetize/cli
appetize skill install
```

Node 22 or later is required. Confirm the install with `appetize --version`.

{% embed url="https://2147444700-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-MJUveBCJfn0GR8-hlqi%2Fuploads%2FVWaXAmAd0n9NlPYz6Noz%2Fclaude-demo-2x.mp4?alt=media&token=8bb00711-1019-43d3-a9ad-579d3da385cf" %}

## Let an agent drive

An agent can create a session and drive a device to complete your tasks:

* "Write the new sign-up copy and give me a screenshot."
* "Reproduce the crash in checkout and give me a screenshot and the device log."
* "Walk the onboarding flow on an iPhone 15 Pro and record it."

### Or drive it yourself

Every command the agent runs, you can run by hand. That is what makes an agent's session debuggable: when it says the tap missed, you can start the same session and look.

### Next steps

* [Getting started](https://docs.appetize.io/agentic-flows/getting-started) — install, token, and your first agent task
* [Sessions](https://docs.appetize.io/agentic-flows/sessions) — lifecycle, logs and network traffic
* [Automation](https://docs.appetize.io/agentic-flows/automation) — inspect the screen and act on it
* [Screenshots and recordings](https://docs.appetize.io/agentic-flows/screenshots-and-recordings) — capture PNGs and MP4s
