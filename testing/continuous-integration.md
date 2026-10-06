# Continuous Integration

Run the same `npx playwright test` command you run locally. Playwright's [CI guide](https://playwright.dev/docs/ci) covers the runner, the reporter, and retries. Two settings are specific to a deployment:

* `baseURL` is the deployment. Cloud is `https://appetize.io`. A self-hosted install is that install's own URL, the same value as the CLI's `APPETIZE_ENDPOINT`.
* `workers` is how many Appetize sessions run at once. Start at `1`.

Keep the test output. A failed run is hard to read without it:

```yaml
- uses: actions/upload-artifact@v4
  if: ${{ !cancelled() }}
  with:
    name: playwright-results
    path: |
      playwright-report/
      test-results/
```

That archive is the HTML report, traces, screenshots, UI hierarchy, and session record. It is separate from the app build, which is uploaded to Appetize and addressed by `buildId`.

Open a downloaded trace with `npx playwright show-trace`. See [Trace Viewer](trace-viewer.md).

The [self-hosted live demo](../guides-and-samples/self-hosted-live-demo.md) walks the whole path on a call: upload the TODO app, drive it from the CLI, run it as a Playwright test, and keep both artifacts.
