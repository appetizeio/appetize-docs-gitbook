# Running Tests

Run your tests exactly as you would in any Playwright project:

```bash
npx playwright test

# or, with the device visible

npx playwright test --headed
```

[See the Playwright documentation for running tests](https://playwright.dev/docs/running-tests)

## Sessions and workers

Every test in a suite runs serially on the **same** Appetize session, for as long as the session configuration stays the same. That avoids re-entering the queue for each test and makes the suite much faster.

A **new session** starts whenever that configuration changes. Each [project](https://docs.appetize.io/testing/projects) has its own config, so a second device or OS version means a second session; so does `test.use({ config })` inside a suite. A failing test also ends its session, and the next suite requests a new one.

`workers` controls how many of those sessions run at once — **each worker holds one Appetize session**, so `workers` is effectively your concurrent session count. Projects created by `npm init @appetize/playwright` start at `workers: 1`.

{% code title="playwright.config.ts" %}
```typescript
// two suites at a time, two concurrent Appetize sessions
workers: 2,
```
{% endcode %}

Raise it only as far as your plan's concurrency allows; beyond that the extra workers sit in the queue. See [Parallelism](https://playwright.dev/docs/test-parallel#worker-processes) in the Playwright docs.

## Running a subset

```bash
# one project
npx playwright test --project=android

# one file
npx playwright test tests/ios/smoke.spec.ts

# anything whose title matches
npx playwright test -g "sign in"

# show what would run, without running it
npx playwright test --list
```

See [Projects](https://docs.appetize.io/testing/projects) for running the same suite across several devices, OS versions or apps.
