# Running Tests

You can run your tests exactly how you would with a regular Playwright project:

```bash
npx playwright test

# or

npx playwright test --headed
```

[See Playwright documentation for running tests](https://playwright.dev/docs/running-tests)

## Parallel Tests

All tests in a test suite will run serially using the same session. This keeps you from re-entering the queue for each individual test and overall leads to faster test times. However, should a test fail, the session ends and a new one is requested.

You may run multiple test suites in parallel so long as your Appetize account has capacity for concurrent sessions. To do this, increase the [number of workers ](https://playwright.dev/docs/test-parallel#worker-processes) in `playwright.config.ts`.

