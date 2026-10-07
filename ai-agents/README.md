---
description: >-
  Agentic mobile testing on simulators. Give an AI coding agent the Appetize CLI
  and let it run, drive and debug your iOS and Android apps.
icon: terminal
---

# AI Agents

Agentic mobile development on simulators: give an AI coding agent the Appetize CLI and let it drive your iOS or Android app.

The `appetize` CLI runs your iOS or Android app on an Appetize device and drives it from your terminal. Sessions are headless (no browser, no embed), so the same commands work on your machine and in CI.

{% hint style="warning" icon="triangle-exclamation" %}
**Beta.** Command names, flags and output are all still changing between releases.
{% endhint %}

```bash
npm install -g @appetize/cli
appetize skill install
```

Node 22 or later is required. Confirm the install with `appetize --version`.

{% embed url="https://cdn.jsdelivr.net/gh/appetizeio/appetize-docs-gitbook@62e4b0e19b02caae039e0fadf43c0a72fbc82cd4/.gitbook/assets/agent-side-by-side.mp4" %}

## Let an agent drive

An agent can take a whole task end to end. Investigate, fix, verify, ship:

* "Take this crash log. Validate it, use the app and network logs to find the root cause, fix it, test it and ship it."
* "Ship the new sign-up copy. Update it, check it on an iPhone 15 Pro and a Pixel 7, and put the screenshots on the PR."
* "Onboarding regressed. Walk it, find where it breaks, fix it, and send me a recording of it working."

Every step is a terminal command, so it loops on its own: change the code, re-run on a simulator, check the recording, repeat. A save can also update the running app, with no rebuild. See [Preview changes without rebuilding](https://docs.appetize.io/guides-and-samples/preview-changes).

### Or drive it yourself

Every command the agent runs, you can run by hand. That is what makes an agent's session debuggable: when it says the tap missed, you can start the same session and look.

### Next steps

* [Getting started](https://docs.appetize.io/ai-agents/getting-started): install, token, and your first agent task
* [Sessions](https://docs.appetize.io/ai-agents/sessions): lifecycle, logs and network traffic
* [Automation](https://docs.appetize.io/ai-agents/automation): inspect the screen and act on it
* [Screenshots and recordings](https://docs.appetize.io/ai-agents/screenshots-and-recordings): capture PNGs and MP4s
* [Preview changes without rebuilding](https://docs.appetize.io/guides-and-samples/preview-changes): save, look, and edit again while the app stays open
