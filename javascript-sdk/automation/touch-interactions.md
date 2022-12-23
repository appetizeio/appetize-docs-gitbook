# Touch interactions

### Targeting Elements

Touch interactions usually require a target element. An element can be described using our Element Selector API; a convenient to way to target a UI element on the device.

A selector is comprised of attributes that describe the element in your application. Below is a list of attributes you can describe for each platform.

{% tabs %}
{% tab title="iOS" %}
| Attribute               | Description                                                                                 |
| ----------------------- | ------------------------------------------------------------------------------------------- |
| accessibilityIdentifier | Value of the element's accessibilityIdentifier                                              |
| baseClass               | <p>Name of the element's base (or inherited) class</p><p></p><p>ex: <code>UIView</code></p> |
| class                   | <p>Name of the element's class<br><br>ex: <code>MyCustomUIView</code></p>                   |
| text                    | Text content of the element and its children (case sensitive)                               |
{% endtab %}

{% tab title="Android" %}
| Attribute    | Description                                                                           |
| ------------ | ------------------------------------------------------------------------------------- |
| class        | <p>Name of the element's class<br><br>ex: <code>android.widget.TextView</code></p>    |
| content-desc | Value of the element's Content Description                                            |
| resource-id  | <p>Value of the element's Resource ID<br><br>ex: <code>com.example:id/icon</code></p> |
| text         | Text content of the element and its children (case sensitive)                         |
{% endtab %}
{% endtabs %}

Any or all of these can be provided at once. If you have multiple elements that share the same attributes (such as "text") you can provide multiple attributes to narrow down the selection.&#x20;

```javascript
await session.tap({
  element: {
    text: "OK",
    class: "UIConfirmButton"
  }  
})
```

If you are a developer for the app, we recommend using accessibility attributes when creating your elements. This will allow for simpler queries and also help your app be more accessible.

```javascript
// ios
await session.tap({
  element: {
      accessibilityIdentifier: "confirm-button"
  }
})

// android
await session.tap({
  element: {
      'content-desc': "confirm button"
  }
})
```

{% hint style="info" %}
Element selectors work regardless of the device or screen size, meaning you can run the same set of actions on both a phone and tablet
{% endhint %}

### findElement

Returns an element that matches the selector. This is useful if you need to wait for an element to appear before doing another action.

```javascript
const element = await session.findElement({
    text: "OK"
})

console.log(element)

// { text: "OK", class: "UIButton", accessbilityIdentifier: 'confirm-btn' }
```

If multiple elements are found it will throw an error. If you want to get all of them you can use [findElements](touch-interactions.md#findelements). Otherwise you can provide an index to get the nth element.

```javascript
// get the first occurence of an element with text "OK"
const element = await session.findElement({
    text: "OK",
    matchIndex: 0
})
```

### findElements

Returns an array of all elements matching that selector. It will error if no elements are found.

```javascript
const elements = await session.findElements({
    text: "OK"
})
```

### swipe()

Swipes at the specified coordinate or element.&#x20;

#### By coordinates

Coordinates can be specified using `px`, `%`, `vw` or `vh` units ([see table below](touch-interactions.md#units)).

```javascript
session.swipe({
    x: '50%',
    y: '50%',
    direction: 'up',
    distance: '10%' // optional (must match unit of x/y)
    duration: 1000 // optional, in ms
})
```

#### By element

```javascript
session.swipe({
    element: { accessibilityIdentifier: 'my-image' },
    direction: 'left',
    distance: '100px' // optional, relative to the top-left of the element
    duration: 1000 // optional, in ms
})
```

#### Units

| Unit | Description                                                    |
| ---- | -------------------------------------------------------------- |
| `px` | Pixels                                                         |
| `%`  | Percentage of screen (or element if targeted) width or height. |
| `vh` | Percentage of the screen height                                |
| `vw` | Percentage of the screen width                                 |

### tap()

Taps on the specified element or coordinates

```javascript
await session.tap({ 
    element: { 
        text: 'submit' 
    }
})
```

```javascript
await session.tap({
    x: 100,
    y: 250
})
```

### type()

Types the given text

```javascript
await session.type("hello")
```

