---
description: >-
  While many users enjoy hassle-free access to Appetize without any network
  adjustments, certain corporate security protocols may restrict connections.
---

# Configure Network Access

For most users there is no need for any network configuration to be able to use Appetize. However, some company's security policies might restrict network access.

## Streaming Server Access

To make sure you can access our streaming servers from behind a firewall:

* [x] Identify your deployment type: Public Cloud or Enterprise Private Cloud Instance.
* [x] Find the IP Blocks used by our streaming servers:
  * For Public Cloud Instances, visit [https://appetize.io/ip-blocks](https://appetize.io/ip-blocks).
  * For Enterprise Private Cloud Instances, visit [https://custom.appetize.io/ip-blocks](https://custom.appetize.io/ip-blocks), replacing 'custom' with your assigned domain.
* [x] Make sure that your network configuration doesn't restrict connectivity to all of the listed IPs.

## Web Server Access

To make sure you can access our web servers from behind a firewall:

* [x] Identify your deployment type: Public Cloud or Enterprise Private Cloud Instance.
* [x] Find your assigned domain name:
  * For Public Cloud Instances, this will be **appetize.io.**
  * For Enterprise Private Cloud Instances, this will be **custom.appetize.io** replacing 'custom' with your assigned domain.
* [x] Ensure all outgoing connections to your domain e.g. **appetize.io** have been whitelisted**.**

{% hint style="info" %}
For our Enterprise Private Cloud Instances, you can also configure which IPs have access to your private instances. [Contact us](https://appetize.io/contact-us) to learn more.
{% endhint %}

## Web Socket Access

Our system relies on WebSockets to communicate with our streaming servers. However, corporate web proxies may block WebSocket connections, preventing you to successfully make use of our service. To ensure proper setup, you can verify your connection using websites like [https://websocketstest.com/](https://websocketstest.com/).

## Storage and Resource Access

To ensure that all necessary static content, scripts, and uploaded resources (such as builds) can be accessed from behind a firewall, please whitelist the following URLs:

* [x] `appetizeio-static.s3.amazonaws.com`
* [x] `appetizeio.s3.amazonaws.com`
* [x] `js.appetize.io`

{% hint style="info" %}
For Enterprise Private Cloud Instances, the URLs will be specific to your organization.  [Contact us](https://appetize.io/support-request) for more information.
{% endhint %}

