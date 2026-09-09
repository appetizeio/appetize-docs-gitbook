---
description: >-
  Run and test mobile apps with AI coding agents — artificial intelligence
  workflows powered by the appetize CLI and its agent skill.
hidden: true
icon: terminal
---

# Agentic Flows

Point an AI coding agent at a real iOS or Android device and let it work.

The `appetize` CLI runs your iOS or Android app on an Appetize device and drives it from your terminal. Sessions are headless — no browser, no embed — so the same commands work on your machine and in CI.

{% hint style="danger" %}
**Beta.** Command names, flags and output are all still changing between releases, so pin the version you install.
{% endhint %}

```bash
npm install -g @appetize/cli@0.15
```

Node 22 or later is required. Confirm the install with `appetize --version`.

<figure><img src="../.gitbook/assets/cli-demo.gif" alt=""><figcaption></figcaption></figure>

## Let an agent drive

With the skill installed, an agent reaches for a device on its own for the tasks that mean exercising the app rather than reading its source: prompts you can give it, in your agent's chat.&#x20;

* "Run this branch on a Pixel 7 and tell me whether the new sign-up copy is live."
* "Reproduce the crash in checkout and send me the screenshot and the device log."
* "Walk the onboarding flow on an iPhone 15 Pro and record it."

What the skill really teaches is the loop that keeps this reliable: inspect the screen, act through selectors, screenshot to verify, and wait by inspecting rather than sleeping. An agent cannot see the device, so guessing at coordinates or sleeping for a few seconds is how these sessions go wrong.

### Or drive it yourself

Every command the agent runs, you can run by hand — same flags, same JSON on stdout. That is what makes an agent's session debuggable: when it says the tap missed, you can start the same session and look.

### Next steps

* [Getting started](https://docs.appetize.io/agentic-flows/getting-started) — install, token, and your first agent task
* [Sessions](https://docs.appetize.io/agentic-flows/sessions) — lifecycle, logs and network traffic
* [Automation](https://docs.appetize.io/agentic-flows/automation) — inspect the screen and act on it
* [Screenshots and recordings](https://docs.appetize.io/agentic-flows/screenshots-and-recordings) — capture PNGs and MP4s
* [Command reference](https://docs.appetize.io/agentic-flows/command-reference) — every command, its values and examples
