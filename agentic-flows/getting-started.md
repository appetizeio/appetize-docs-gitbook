# Getting started

## 1. Install the CLI

```bash
npm install -g @appetize/cli
appetize --version
```

Node 22 or later is required.

## 2. Set your API token

Create a token in your [organization settings](https://docs.appetize.io/account/api-tokens) and export it:

```bash
export APPETIZE_API_TOKEN=tok_xxxxxxxxxxxx
```

## 3. Install the skill for your AI agent

```bash
appetize skill install
```

The skill is installed for each agent whose directory is already in your project: Claude Code reads `.claude/skills`, and Codex, Copilot and Cursor read `.agents/skills`. When neither is found, both are written.

```bash
appetize skill install --scope user                  # install in your home directory
appetize skill install --agent claude --agent cursor # choose the agents yourself
```

It teaches the session lifecycle, how to match elements by test id and text, when to inspect and when to screenshot, and how to wait on an element instead of sleeping.

## 4. Give your agent a task

Ask for something that needs the app running, and name the device and build if you care which:

> Run build `b_a1b2c3` on a Pixel 7, tap through to the checkout screen and screenshot it.

The agent will find a target with `appetize build list`, start a session, inspect the screen to locate elements, act through selectors, screenshot each meaningful step, and stop the session when it's done.

{% hint style="info" %}
A session holds a device for as long as it runs. If an agent leaves one behind, `appetize session stop` releases it.
{% endhint %}

## 5. Drive it yourself

Every command the agent runs works by hand:

```bash
appetize device list --platform android   # device ids and their OS versions
appetize build list                       # your builds; each id is a target
appetize session start pixel7 b_a1b2c3
appetize inspect                          # what is on screen
appetize tap --select-text 'Log in'
appetize screenshot after-login
appetize session stop
```

`session start` prints the session as JSON — the id, the streaming host and the log paths. Everything after it acts on that session, so there is no id to pass.
