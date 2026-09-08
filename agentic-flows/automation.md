# Automation

You cannot see the device, so `inspect` and `screenshot` are your eyes. The loop that works: inspect to find an element, act on it by selector, screenshot to confirm.

## Inspect the screen

```bash
appetize inspect
appetize inspect --select-test-id login-form --pretty
```

The hierarchy is written to `inspect.json` — name a path to choose another file — and a summary is printed:

```json
{
  "bytes": 11551,
  "nodes": 44,
  "output": "inspect.json"
}
```

The JSON is `{ platform, root }`, where each node carries `attributes`, `bounds` and `children`. Only what is on screen right now appears: an element scrolled away or covered is not in the tree, so absence means "not visible", not "does not exist".

{% hint style="info" %}
An unscoped hierarchy runs past 100 KB on an ordinary screen. Scope it with a selector and read the file rather than dumping it to the terminal.
{% endhint %}

## Selectors

Match what an element is, not where it happens to sit.

| Flag                       | Matches                                                                            |
| -------------------------- | ---------------------------------------------------------------------------------- |
| `--select-test-id`         | Android `resource-id` or iOS `accessibilityIdentifier`, exact                      |
| `--select-text`            | An exact string, or `/regex/flags` such as `/sign in/i`                            |
| `--select-index`           | Which match when several, 0-based                                                  |
| `--select-position`        | A screen position as `x,y`, each 0-1                                               |
| `--select-x`, `--select-y` | A point within the matched element (0-1; outside that range reaches past its edge) |

Pick one of `--select-test-id`, `--select-text` or `--select-position`. A test id is the most durable, then text. Coordinates are right for canvases, maps and slider tracks, and wrong everywhere else — a selector survives a layout change and a coordinate does not.

`swipe` names two points, so it takes the same suffixes under `--from-*` and `--to-*`.

## Tap, type and press

```bash
appetize tap --select-test-id save
appetize tap --select-text 'Log in'
appetize tap --select-text '/^item \d+/i' --select-index 2
appetize tap --select-position 0.5,0.75
```

```bash
appetize type 'user@example.com{Tab}hunter2{Enter}'
appetize type '{Backspace>16/}'
```

Typing does not focus a field — tap it first. In `type`, `{...}` names a key (`Enter`, `Tab`, `Backspace`, the arrows), `{Backspace>16/}` repeats one 16 times, and `{{` types a literal `{`.

```bash
appetize press home
appetize press back
appetize rotate landscapeLeft
```

`home` and `lock` work on both platforms; `back`, `menu`, `unlock`, `volumeUp` and `volumeDown` are Android only.

## Swipe

Scroll the screen with `--direction`, optionally from a starting point:

```bash
appetize swipe --direction up
appetize swipe --direction up --distance 0.25
appetize swipe --direction left --from-test-id card --from-index 1
```

Drag along a path by naming both ends — this is how you reorder a list or drop something on a target:

```bash
appetize swipe --from-test-id card-3 --to-test-id archive-bin
appetize swipe --from-text 'Drag me' --from-y 0.9 --to-test-id drop-zone
```

## Wait for an element, don't sleep

```bash
appetize inspect --select-test-id home-feed --timeout 5000
```

`--timeout` waits for the element and exits non-zero if it never appears, which makes it a wait primitive: it returns the moment the element is there, and fails clearly when it isn't. `tap` and `swipe` take it too. Sleeping guesses, and guesses are either slow or flaky.

## Dismiss the keyboard

There is no keyboard-dismiss command, and tapping an inert element only clears focus if the app wired that up. Press the return key on iOS, and back on Android — while the keyboard is up, back dismisses it instead of navigating:

```bash
appetize type '{Enter}'   # iOS
appetize press back       # Android
```

Both leave you on the same screen. Confirm with `inspect`: the keyboard's own nodes disappear once it is down.

## Watch an agent do it

A real Claude Code session driving a device with these commands. It inspects the screen, taps through two permission dialogs it did not expect, screenshots the file list, then stops the session — about 45 seconds end to end.

<figure><img src="../.gitbook/assets/claude-drives-device (1).gif" alt=""><figcaption></figcaption></figure>
