---
description: >-
  Get IP blocks for Appetize streaming servers. These are the IPs from which
  your running apps will be making network call. Use the IP blocks to whitelist
  access to your backend if it is not public.
---

# IP Blocks

{% swagger baseUrl="https://appetize.io" path="/ip-blocks" method="get" summary="Get IP blocks" expanded="true" %}
{% swagger-description %}
Get IP blocks for Appetize streaming servers. These are the IPs from which your running apps will be making network calls. Use the IP blocks to whitelist access to your backend if it is not public.
{% endswagger-description %}

{% swagger-response status="200" description="" %}
```javascript
{
    "ipv4": [
        "63.135.170.0/24",
        "66.55.157.0/24",
        "66.185.22.0/24",
        "73.15.222.0/24",
        "95.141.32.0/21"
    ]
}
```
{% endswagger-response %}
{% endswagger %}
