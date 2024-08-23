---
description: >-
  Appetize supports simulating device location for running and testing
  location-based applications easily.
---

# Mock Location

### With Query Parameter

To specify the device location, include the `location` query parameter in your app or embed URL, followed by the latitude and longitude values e.g.

```uri
&location=-33.924434,18.418391
```

See [Query Params Reference](../platform/query-params-reference.md#location) for more information.

### With JavaScript SDK

Set the location of the device via our JavaScript SDK

#### With Configuration

Specify the location by passing in a number array in format `[latitude, longitude]` e.g.

```typescript
await client.setConfig({
    location: [-33.924434, 18.418391],
    ...
})
```

See [Configuration](../javascript-sdk/configuration.md#location) for more information.

#### With setLocation()

Specify the location by passing in the number parameters `latitude` and `longitude` e.g.

```typescript
await setLocation(-33.924434, 18.418391)
```

See the [API Reference](../javascript-sdk/api-reference.md#setlocation) for more information.
