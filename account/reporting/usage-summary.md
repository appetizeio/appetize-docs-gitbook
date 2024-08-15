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

<figure><img src="../../.gitbook/assets/image (59).png" alt="" width="368"><figcaption><p>Select "Download" under Monthly or Daily usage report</p></figcaption></figure>

### With REST API

You can access your usage report via our REST API. For more information, see

{% content-ref url="../../rest-api/usage-summary.md" %}
[usage-summary.md](../../rest-api/usage-summary.md)
{% endcontent-ref %}

## Glossary

{% hint style="warning" %}
Please note, depending on the activity and actions you take within Appetize, not all fields may be populated in your reports.
{% endhint %}

| Field                                           | Description                                                                                                                   |
| ----------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| <h4><strong>month</strong></h4>                 | The month being reported on                                                                                                   |
| <h4><strong>publicKey</strong></h4>             | The App's publicKey                                                                                                           |
| <h4><strong>numSessions</strong></h4>           | How many sessions were run that month/day on that publicKey                                                                   |
| <h4><strong>minutes</strong></h4>               | How many total minutes for that day/month                                                                                     |
| <h4><strong>platform</strong></h4>              | _iOS_ or _Android_                                                                                                            |
| <h4><strong>name_latest</strong></h4>           | <p>The current name of the app</p><p><br><strong>NOTE</strong>: May differ from when the app was run</p>                      |
| <h4><strong>appdisplayname_latest</strong></h4> | <p>The current display name of the app</p><p><br><strong>NOTE</strong>: May differ from when the app was run</p>              |
| <h4><strong>bundle_latest</strong></h4>         | <p>The current <em>bundleId</em> of the app</p><p><br><strong>NOTE</strong>: May differ from when the app was run</p>         |
| <h4><strong>note_latest</strong></h4>           | <p>The current notes for the app from the dashboard</p><p><br><strong>NOTE</strong>: May differ from when the app was run</p> |

{% hint style="info" %}
Should you have a desire to report on additional fields, please [reach out to us](mailto:hello@appetize.io) and we'll consider it for our roadmap.
{% endhint %}
