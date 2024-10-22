---
description: >-
  Appetize provides daily and monthly usage reports to give users insight into
  what's happening within their instance.
---

# Usage Summary

### With Reporting Page

You can access your usage summary by navigating to your [Reports Dashboard](https://appetize.io/reports) and selecting **download** under:

* **Monthly usage report**
* **Daily usage report** after specifying the month that you are interested in e.g. May 2023

<figure><img src="../../.gitbook/assets/image (66).png" alt="" width="368"><figcaption><p>Select "Download" under Monthly or Daily usage report</p></figcaption></figure>

{% hint style="info" %}
All reports are downloaded in UTC (Coordinated Universal Time) times.
{% endhint %}

### With REST API

You can access your usage report via our REST API. For more information, see

{% content-ref url="../../rest-api/usage-summary.md" %}
[usage-summary.md](../../rest-api/usage-summary.md)
{% endcontent-ref %}

## Glossary

{% hint style="warning" %}
Please note, depending on the activity and actions you take within Appetize, not all fields may be populated in your reports.
{% endhint %}

| Field                      | Description                                                                                                                   |
| -------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| **month**                  | The month being reported on                                                                                                   |
| **publicKey**              | The App's publicKey                                                                                                           |
| **numSessions**            | How many sessions were run that month/day on that publicKey                                                                   |
| **minutes**                | How many total minutes for that day/month                                                                                     |
| **platform**               | _iOS_ or _Android_                                                                                                            |
| **name\_latest**           | <p>The current name of the app</p><p><br><strong>NOTE</strong>: May differ from when the app was run</p>                      |
| **appdisplayname\_latest** | <p>The current display name of the app</p><p><br><strong>NOTE</strong>: May differ from when the app was run</p>              |
| **bundle\_latest**         | <p>The current <em>bundleId</em> of the app</p><p><br><strong>NOTE</strong>: May differ from when the app was run</p>         |
| **note\_latest**           | <p>The current notes for the app from the dashboard</p><p><br><strong>NOTE</strong>: May differ from when the app was run</p> |

{% hint style="info" %}
Should you have a desire to report on additional fields, please [reach out to us](mailto:hello@appetize.io) and we'll consider it for our roadmap.
{% endhint %}
