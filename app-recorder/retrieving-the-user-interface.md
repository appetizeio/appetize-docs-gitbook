# Retrieving the user interface

The app recorder uses an XML representation of your app's user interface. You may find it helpful to retrieve this data (UI Dump) to programmatically understand what your app is displaying.

Send a cross-document message with the value `dumpUi`, for example `window.postMessage('dumpUi', '*')`. When the UI Dump is ready, the iframe will post a message with `type` set to `uiDump`. The `value` field will be an object with a `result` string field that contains the XML that represents your app's current user interface. For example:

```javascript
// example event.data received by cross-document message handler
{
    "type": "uiDump",
    "value": {
        "result": "<?xml version='1.0' encoding='UTF-8' ?>..."
    }
}
```
