# Trace Viewer

The [Playwright Trace Viewer](https://playwright.dev/docs/trace-viewer-intro) allows you to review the playback of your test. This can be recorded locally, or downloaded from CI when a test fails.

It is designed for web tests, so while the features like network logging and DOM inspection will not work for Appetize, you can still use it to look at the video recording of the test.

{% code title="playwright.config.ts" %}
```typescript
const config = {
  ...
  use: {
    trace: 'retain-on-failure'
  },
}
```
{% endcode %}
