# Trace Viewer

The [Playwright Trace Viewer](https://playwright.dev/docs/trace-viewer-intro) allows you to review the playback of your test. This can be recorded locally, or downloaded from CI when a test fails.

It is designed for web tests, so while the features like network logging and DOM inspection will not work for Appetize, you can still use it to look at the video recording of the test.

We recommend enabling tracing with `on-first-retry` mode as we have found `on` and `retain-on-failure` to hinder performance of tests.

```typescript
// playwright.config.ts
import type { PlaywrightTestConfig } from '@playwright/test';
const config: PlaywrightTestConfig = {
  ...
  use: {
    trace: 'on-first-retry', // record traces on first retry of each test
  },
};
export default config;
```
