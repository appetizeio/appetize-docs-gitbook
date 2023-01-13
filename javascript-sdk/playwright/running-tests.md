# Running Tests

You can run your tests exactly how you would with a regular Playwright project:

```bash
npx playwright test

# or

npx playwright test --headed
```

[See Playwright documentation for running tests](https://playwright.dev/docs/running-tests)

## Parallel Tests

Appetize will only run 1 session for all tests in a test suite. This allows you to use the same device for your tests and keeps you from re-entering the queue for each individual test.

However you may run multiple test suites at once so long as your Appetize account has capacity for concurrent sessions. If not, you will simply enter the queue and the test will proceed once you have a session (tests will increase their timeout to 5 minutes if you enter a queue).

To do this, edit the [worker configuration](https://playwright.dev/docs/test-parallel#worker-processes) in `playwright.config.ts`.&#x20;

## Continuous Integration

[See Playwright documentation for running on CI](https://playwright.dev/docs/ci)
