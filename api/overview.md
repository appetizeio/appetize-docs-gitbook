# Overview

All users with _admin_ or _developer_ roles may request an API token after logging in at [https://appetize.io/account](https://appetize.io/account).  

All HTTP POST requests must use JSON. All responses will be in JSON.

### HTTP responses

| Status code | Details |
| :--- | :--- |
| 200 | OK - Everything worked as expected. |
| 400 | Bad Request - Often missing a required parameter. |
| 401 | Unauthorized - No valid API token provided. |
| 404 | Not Found - No app found for publicKey specified. |
| 500, 502, 503, 504 | Server error - something went wrong on our server. |

_Note: If you are using an enterprise private instance of Appetize.io. please replace all API calls from api.appetize.io to your custom domain, eg. custom.appetize.io._ 



