---
description: >-
  Keep your passwords secure on Android with Appetize's Hide Password Visibility
  feature that ensures your passwords are hidden from view.
---

# Hide Password Visibility

### With Query Parameter

Add the `hidePasswords=true` query parameter to your app or embed URL

```uri
&hidePasswords=true
```

See [Query Params Reference](../../../platform/query-params-reference.md#hidepasswords) for more information.

### With JavaScript SDK

Set `hidePasswords: true` in the configuration e.g.

```typescript
await client.setConfig({
    hidePasswords: true,
    ...
})
```

See [Configuration](../../../javascript-sdk/configuration.md#hidepasswords) for more information.
