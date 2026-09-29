# Screenshots and recordings

## Screenshots

```bash
appetize screenshot
appetize screenshot after-login
appetize screenshot ./shots/checkout.png
```

A PNG is written and its details printed:

```json
{
  "bytes": 99525,
  "mimeType": "image/png",
  "output": "after-login.png"
}
```

The name is optional — it defaults to `screenshot` — and the extension is added for you. Take one after each meaningful step: a tap that "succeeded" only means the gesture was delivered, not that the app did what you expected.

## Video

Video is opt-in. Nothing streams from the device until you start recording:

```bash
appetize recording start login-flow
# ... drive the app ...
appetize recording stop
```

`recording start` has the daemon open the video stream and write it to the file you name, printing the path. The name is required, `.mp4` is added if you omit it, and the directory must already exist. `recording stop` closes the stream and the file.

Recording over an existing file fails unless you pass `--force`, so name a new file to record twice in one session. Starting a second recording while one is running also fails, so a recording always begins where you asked it to.

Ending the session while recording closes the file cleanly, and a session that dies unexpectedly still leaves the file playable, losing at most the last second.

## See it run

The same session from both sides: the commands on the left, the device video they produced on the right. recording start opens the stream, the taps and typing land on the device, and recording stop closes the file.

{% embed url="https://2147444700-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-MJUveBCJfn0GR8-hlqi%2Fuploads%2FsX3n8XF0SlMNdbVGzbxP%2Frecording-side-by-side.mp4?alt=media&token=5bfcbbd7-dad3-4d10-810c-917e946fa685" %}
