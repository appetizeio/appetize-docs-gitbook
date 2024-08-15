---
description: >-
  Appetize provides monthly session history reports to give users insight into
  what's happening within their instance, including which logged-in user ran
  that session.
---

# Session History

### With Reporting Page

You can access your session history by navigating to your [Reports Dashboard](https://appetize.io/reports) and selecting **download** under session logs after specifying the month that you are interested in:

<figure><img src="../../.gitbook/assets/image (58).png" alt="" width="365"><figcaption><p>Select "Download" under session logs after specifying the month you are interested in</p></figcaption></figure>

## Glossary

{% hint style="warning" %}
Please note, depending on the activity and actions you take within Appetize, not all fields may be populated in your reports.
{% endhint %}

| Field                                               | Description                                                                                                                                                                                   |
| --------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <h4><strong>reportStartDate</strong></h4>           | The starting date of the report.                                                                                                                                                              |
| <h4><strong>reportEndDate</strong></h4>             | The ending date of the report.                                                                                                                                                                |
| <h4><strong>publicKey</strong></h4>                 | Public key of the app associated with the session                                                                                                                                             |
| <h4><strong>sessionRequested</strong></h4>          | <p>When the session was requested.<br><strong>NOTE</strong>: May differ from session start time if there was a queue</p>                                                                      |
| <h4><strong>startTime</strong></h4>                 | When the session started                                                                                                                                                                      |
| <h4><strong>userConnected</strong></h4>             | When the user connected to the streaming server - should be shortly after _startTime._                                                                                                        |
| <h4><strong>frameTime</strong></h4>                 | When the user received the first frame from the streaming server.                                                                                                                             |
| <h4><strong>appLaunchTime</strong></h4>             | When the app was launched - should be similar to _frameTime._                                                                                                                                 |
| <h4><strong>endTime</strong></h4>                   | When the session ended.                                                                                                                                                                       |
| <h4><strong>closeTime</strong></h4>                 | <p>Session end time plus time to shut down and reset the simulator.<br><strong>NOTE</strong>: This is what we bill on for our metered usage customers using our Starter or Premium Plans.</p> |
| <h4><strong>sessionLengthMilliseconds</strong></h4> | Duration of the session in milliseconds.                                                                                                                                                      |
| <h4><strong>sessionLengthSeconds</strong></h4>      | Duration of the session in seconds.                                                                                                                                                           |
| <h4><strong>sessionLengthMinutes</strong></h4>      | Duration of the session in minutes.                                                                                                                                                           |
| <h4><strong>referrer</strong></h4>                  | The URL that brought the user to the app page, or the URL that embedded the app.                                                                                                              |
| <h4><strong>referrerHostname</strong></h4>          | Hostname of the referrer.                                                                                                                                                                     |
| <h4><strong>token</strong></h4>                     | A unique random identifier for this streaming session.                                                                                                                                        |
| <h4><strong>clientIP</strong></h4>                  | IP address of the user running the session.                                                                                                                                                   |
| <h4><strong>clientLanguage</strong></h4>            | System Language of user running the session.                                                                                                                                                  |
| <h4><strong>clientUserAgent</strong></h4>           | The user agent string that identifies the user's browser.                                                                                                                                     |
| <h4><strong>versionCode</strong></h4>               | <p>Which build of the app was run.<br><strong>NOTE:</strong> <em>Starts at 1 and increments each time the app is updated.</em></p>                                                            |
| <h4><strong>deviceType</strong></h4>                | Type of the device being used for this session.                                                                                                                                               |
| <h4><strong>osVersion</strong></h4>                 | Operating System being used for this session.                                                                                                                                                 |
| <h4><strong>rotation</strong></h4>                  | What orientation the device was in on session start (e.g., portrait, landscape).                                                                                                              |
| <h4><strong>debug</strong></h4>                     | Whether debug logging was used.                                                                                                                                                               |
| <h4><strong>warmSession</strong></h4>               | Whether the session was served from a reserved device.                                                                                                                                        |
| <h4><strong>queued</strong></h4>                    | Whether the user was queued before the session started.                                                                                                                                       |
| <h4><strong>noVideo</strong></h4>                   | If video was disabled, usually for headless usage.                                                                                                                                            |
| <h4><strong>location</strong></h4>                  | The manually specified GPS location for the emulator/simulator, if provided.                                                                                                                  |
| <h4><strong>appetizeUser</strong></h4>              | Username of the user associated with the session, if logged in.                                                                                                                               |

{% hint style="info" %}
Should you have a desire to report on additional fields, please [reach out to us](mailto:hello@appetize.io) and we'll consider it for our roadmap.
{% endhint %}
