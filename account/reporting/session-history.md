---
description: >-
  Appetize provides monthly session history reports to give users insight into
  what's happening within their instance, including which logged-in user ran
  that session.
---

# Session History

### With Reporting Page

You can access your session history by navigating to your [Reports Dashboard](https://appetize.io/reports) and selecting **download** under session logs after specifying the month that you are interested in:

<figure><img src="../../.gitbook/assets/image (65).png" alt="" width="365"><figcaption><p>Select "Download" under session logs after specifying the month you are interested in</p></figcaption></figure>

{% hint style="info" %}
All reports are downloaded in UTC (Coordinated Universal Time) times.
{% endhint %}

## Glossary

{% hint style="warning" %}
Please note, depending on the activity and actions you take within Appetize, not all fields may be populated in your reports.
{% endhint %}

| Field                         | Description                                                                                                                                                                                   |
| ----------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **reportStartDate**           | The starting date of the report.                                                                                                                                                              |
| **reportEndDate**             | The ending date of the report.                                                                                                                                                                |
| **publicKey**                 | Public key of the app associated with the session                                                                                                                                             |
| **sessionRequested**          | <p>When the session was requested.<br><strong>NOTE</strong>: May differ from session start time if there was a queue</p>                                                                      |
| **startTime**                 | When the session started                                                                                                                                                                      |
| **userConnected**             | When the user connected to the streaming server - should be shortly after _startTime._                                                                                                        |
| **frameTime**                 | When the user received the first frame from the streaming server.                                                                                                                             |
| **appLaunchTime**             | When the app was launched - should be similar to _frameTime._                                                                                                                                 |
| **endTime**                   | When the session ended.                                                                                                                                                                       |
| **closeTime**                 | <p>Session end time plus time to shut down and reset the simulator.<br><strong>NOTE</strong>: This is what we bill on for our metered usage customers using our Starter or Premium Plans.</p> |
| **sessionLengthMilliseconds** | Duration of the session in milliseconds.                                                                                                                                                      |
| **sessionLengthSeconds**      | Duration of the session in seconds.                                                                                                                                                           |
| **sessionLengthMinutes**      | Duration of the session in minutes.                                                                                                                                                           |
| **referrer**                  | The URL that brought the user to the app page, or the URL that embedded the app.                                                                                                              |
| **referrerHostname**          | Hostname of the referrer.                                                                                                                                                                     |
| **token**                     | A unique random identifier for this streaming session.                                                                                                                                        |
| **clientIP**                  | IP address of the user running the session.                                                                                                                                                   |
| **clientLanguage**            | System Language of user running the session.                                                                                                                                                  |
| **clientUserAgent**           | The user agent string that identifies the user's browser.                                                                                                                                     |
| **versionCode**               | <p>Which build of the app was run.<br><strong>NOTE:</strong> <em>Starts at 1 and increments each time the app is updated.</em></p>                                                            |
| **deviceType**                | Type of the device being used for this session.                                                                                                                                               |
| **osVersion**                 | Operating System being used for this session.                                                                                                                                                 |
| **rotation**                  | What orientation the device was in on session start (e.g., portrait, landscape).                                                                                                              |
| **debug**                     | Whether debug logging was used.                                                                                                                                                               |
| **warmSession**               | Whether the session was served from a reserved device.                                                                                                                                        |
| **queued**                    | Whether the user was queued before the session started.                                                                                                                                       |
| **noVideo**                   | If video was disabled, usually for headless usage.                                                                                                                                            |
| **location**                  | The manually specified GPS location for the emulator/simulator, if provided.                                                                                                                  |
| **appetizeUser**              | Username of the user associated with the session, if logged in.                                                                                                                               |

{% hint style="info" %}
Should you have a desire to report on additional fields, please [reach out to us](mailto:hello@appetize.io) and we'll consider it for our roadmap.
{% endhint %}
