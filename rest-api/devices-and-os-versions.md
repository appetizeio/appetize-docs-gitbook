---
description: List of available devices and operating systems.
---

# Devices & OS Versions

{% swagger baseUrl="https://appetize.io" path="/available-devices" method="get" summary="Get available devices" expanded="true" %}
{% swagger-description %}
Get the list of available devices and operating systems.
{% endswagger-description %}

{% swagger-response status="200" description="" %}
```javascript
{
    "ios": {
        "iphone4s": ["8.4", "9.3"],
        "iphone5s": ["8.4", "9.3", "10.3", "11.4", "12.2"],
        "iphone6": ["8.4", "9.3", "10.3", "11.4", "12.2"],
        "iphone6plus": ["8.4", "9.3", "10.3", "11.4", "12.2"],
        "iphone6s": ["9.3", "10.3", "11.4", "12.2", "13.3", "14.0"],
        "iphone6splus": ["9.3", "10.3", "11.4", "12.2", "13.3", "14.0"],
        "iphone7": ["10.3", "11.4", "12.2", "13.3", "14.0"],
        "iphone7plus": ["10.3", "11.4", "12.2", "13.3", "14.0"],
        "iphone8": ["11.4", "12.2", "13.3", "14.0"],
        "iphone8plus": ["11.4", "12.2", "13.3", "14.0"],
        "iphonex": ["11.4", "12.2", "13.3", "14.0"],
        "iphonexs": ["12.2", "13.3", "14.0"],
        "iphonexsmax": ["12.2", "13.3", "14.0"],
        "iphone11pro": ["13.3", "14.0"],
        "iphone11promax": ["13.3", "14.0"],
        "ipadair": ["8.4", "9.3", "10.3", "11.4", "12.2"],
        "ipadair2": ["9.3", "10.3", "11.4", "12.2", "13.3", "14.0"]
    },
    "android": {
        "nexus5": ["4.4", "5.1", "6.0", "7.1", "8.1", "9.0", "10.0", "11.0"],
        "nexus7": ["4.4", "5.1", "6.0", "7.1", "8.1", "9.0", "10.0", "11.0"],
        "nexus9": ["4.4", "5.1", "6.0", "7.1", "8.1", "9.0", "10.0", "11.0"],
        "pixel4": ["10.0", "11.0"],
        "pixel4xl": ["10.0", "11.0"],
        "galaxytabs7": ["10.0", "11.0"],
        "hammerhead": ["6.0.1"]
    }
}
```
{% endswagger-response %}
{% endswagger %}
