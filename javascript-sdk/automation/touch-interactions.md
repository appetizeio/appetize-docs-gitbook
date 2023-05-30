# Touch interactions

## Targeting Elements

Touch interactions will usually require a target element. An element can be described using our Element Selector API; a convenient to way to target a UI element on the device.

A selector is comprised of attributes that describe the element in your application. Below is a list of attributes you can describe for each platform.

{% hint style="info" %}
Element selectors work regardless of the device or screen size, meaning you can run the same set of actions on both a phone and tablet
{% endhint %}

{% tabs %}
{% tab title="iOS" %}
| Attribute               | Description                                                                                                                                            |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| accessibilityIdentifier | The element's [accessibilityIdentifier](https://developer.apple.com/documentation/uikit/uiaccessibilityidentification/1623132-accessibilityidentifier) |
| accessibilityLabel      | The element's [accessibilityLabel](https://developer.apple.com/documentation/objectivec/nsobject/1615181-accessibilitylabel)                           |
| accessibilityHint       | The element's [accessibilityHint](https://developer.apple.com/documentation/objectivec/nsobject/1615093-accessibilityhint)                             |
| accessibilityValue      | The element's [accessibilityValue](https://developer.apple.com/documentation/objectivec/nsobject/1615117-accessibilityvalue)                           |
| baseClass               | Name of the element's base (or inherited) class                                                                                                        |
| class                   | Name of the element's class                                                                                                                            |
| text                    | Text content of the element and its children (case sensitive)                                                                                          |
{% endtab %}

{% tab title="Android" %}
| Attribute    | Description                                                                           |
| ------------ | ------------------------------------------------------------------------------------- |
| resource-id  | <p>Value of the element's Resource ID<br><br>ex: <code>com.example:id/icon</code></p> |
| content-desc | Value of the element's Content Description (case sensitive)                           |
| class        | <p>Name of the element's class<br><br>ex: <code>android.widget.TextView</code></p>    |
| text         | Text content of the element and its children (case sensitive)                         |
{% endtab %}
{% endtabs %}

Any mixture of these attributes can be used to describe your element:

```javascript
// tap on an element by text
await session.tap({
  element: {
    attributes: { 
      text: "OK"
    }
  }  
})

// tap on an element by accessibilityIdentifier
await session.tap({
  element: {
    attributes: {
      accessibilityIdentifier: "dialog-confirm-button"
    }
  }  
})

// tap on an element by *both* text and accessibilityIdentifier
await session.tap({
  element: {
    text: "OK",
    accessibilityIdentifier: "dialog-confirm-button"
  }  
})
```

## Best Practices

When developing your app, we recommend adding accessibility identifiers wherever possible to aid you when automating interactions with Appetize. This will allow for simpler queries and also help your app be more accessible.

On iOS, you should be using **`accessibilityIdentifier`**.

On Android, you should be using **`resource-id`**.

If you are using React Native, a **`testID`** prop on your component will map to `accessibilityIdentifier` on iOS and `resource-id` on Android.

```javascript
// ios
await session.tap({
  element: {
      attributes: {
          accessibilityIdentifier: "dialog-confirm-button"
      }
  }
})

// android
await session.tap({
  element: {
      attributes: {
          'resource-id': "dialog-confirm-button"
      }
  }
})
```

{% hint style="info" %}
If you do not have an **accessibilityId** to reference it is best to query elements by text or accessibility attributes such as **`accessibilityLabel`** (iOS) or **`content-desc`** (Android).
{% endhint %}

## Methods

### findElement

Returns an element that matches the selector. This is useful for waiting until an element appears.

```javascript
const element = await session.findElement({
    text: "Home"
})

console.log(element)

// output
{
  attributes: { text: "Home", class: "UILabel" },
  path: "0/0/0/0/1/2/3",
  bounds: { x: 10, y: 100, width: 100, height: 20 }  
}
```

If multiple elements are found it will return the first element.

### findElements

Returns an array of all elements matching that selector.

```javascript
const elements = await session.findElements({
    accessibilityLabel: 'Like post'
})
```

### swipe

Swipes from the screen position or element

#### By position or coordinates

```javascript
// swipe up at middle of the screen
session.swipe({
    gesture: 'up', // can be 'left', 'down', 'right', or a function
    position: {
        x: '50%', // 50% of screen width
        y: '50%', // 50% of screen height
    },
    duration: 1000 // optional, in ms
})

// swipe up at x/y coordinate
session.swipe({
    gesture: 'up',
    coordinates: {
        x: 100,
        y: 100
    }
})
```

#### By element

```javascript
// swipe left from the middle of an image element
session.swipe({
    gesture: 'left'
    element: { 
        attributes: {
            accessibilityIdentifier: 'image-carousel' 
        }        
    },
    // optional, defaults to 50%,50%
    localPosition: { 
        x: '50%', // middle of element on x-axis
        y: '50%'  // middle of element on y-axis
    }
})
```

#### Complex Gestures

You can describe a more complex gesture by providing a function to `gesture`.&#x20;

```javascript
// swipe from middle of screen to the left and then down
session.swipe({
    position: {
        x: '50%',
        y: '50%',
    },
    // use up(), left(), right(), or down() for simple movements
    gesture: g => g.left('25%').down('25%')
})

// swipe diagonally up and right
session.swipe({
    position: {
        x: '50%',
        y: '50%',
    },
    // .to(x, y) will move to that position on screen
    gesture: g => g.to('25%', '-25%')
})

// swipe up, wait 500ms, and then swipe right
session.swipe({
    position: {
        x: '0%',
        y: '100%',
    },
    // wait(ms) will hold the swipe gesture in place
    gesture: g => g.up('25%').wait(500).right('50%')
})
```

### tap

Taps on the specified element or coordinates

#### By position or coordinate

```javascript
// tap at middle of the screen
await session.tap({
    position: {
        x: '50%',
        y: '50%'
    }
})

// tap at x/y coordinate
await session.tap({
    position: {
        x: 100,
        y: 250
    }
})
```

#### By element

```javascript
await session.tap({ 
    element: {
        attributes: {
            text: 'submit'
        } 
    }
})
```

## Timeouts

Interactions that target an element will wait up to 10 seconds to find the element. You may lower these timeouts by passing a second parameter:

```javascript
await session.tap({ ... }, { timeout: 5000 })
await session.swipe({ ... }, { timeout: 5000 })
await session.findElement({ ... }, { timeout: 5000 })
```
