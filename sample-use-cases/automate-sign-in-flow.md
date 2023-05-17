---
description: Automate signing in with username and password
---

# Automate Sign-in Flow



```typescript
const session = await client.startSession()

// fills in username, password and then taps "Login" button
async function login(username, password) {
    // type username
    await session.tap({ element: { accessibilityIdentifier: 'username_field' } })
    await session.type({ value: username })
    
    // type password
    await session.tap({ element: { accessibilityIdentifier: 'password_field' } })
    await session.type({ value: password })
    
    // tap login button
    await session.tap({ element: { text: 'Login' } })
}

// login!
await login("john@doe.com", "securepassword")
```
