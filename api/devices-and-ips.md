# Devices and IPs

{% api-method method="get" host="https://appetize.io" path="/available-devices" %}
{% api-method-summary %}
Get available devices
{% endapi-method-summary %}

{% api-method-description %}
Get the list of available devices and operating systems.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

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
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://appetize.io" path="/ip-blocks" %}
{% api-method-summary %}
Get IP blocks
{% endapi-method-summary %}

{% api-method-description %}
Get IP blocks for Appetize.io streaming servers. These are the IPs from which your running apps will be making network calls. 
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

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
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

