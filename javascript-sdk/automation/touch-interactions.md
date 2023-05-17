# Touch interactions

## Targeting Elements

Touch interactions will usually require a target element. An element can be described using our Element Selector API; a convenient to way to target a UI element on the device.

A selector is comprised of attributes that describe the element in your application. Below is a list of attributes you can describe for each platform.

{% hint style="info" %}
Element selectors work regardless of the device or screen size, meaning you can run the same set of actions on both a phone and tablet
{% endhint %}

{% tabs %}
{% tab title="iOS" %}
| Attribute               | Description                                                                          |
| ----------------------- | ------------------------------------------------------------------------------------ |
| accessibilityIdentifier | Value of the element's accessibilityIdentifier                                       |
| accessibilityLabel      | Value of the element's accessibilityLabel                                            |
| baseClass               | <p>Name of the element's base (or inherited) class</p><p>ex: <code>UIView</code></p> |
| class                   | <p>Name of the element's class<br><br>ex: <code>MyCustomUIView</code></p>            |
| text                    | Text content of the element and its children (case sensitive)                        |
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
    text: "OK"
  }  
})

// (iOS) tap on an element by accessibilityIdentifier
await session.tap({
  element: {
    accessibilityIdentifier: "dialog-confirm-button"
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

On iOS, you should be using `accessibilityIdentifier`.

On Android, you should be using `content-desc` or `resource-id`.

If you are using React Native, a `testID` prop on your component will map to `accessibilityIdentifier` on iOS and `resource-id` on Android.

```javascript
// ios
await session.tap({
  element: {
      accessibilityIdentifier: "dialog-confirm-button"
  }
})

// android
await session.tap({
  element: {
      'resource-id': "dialog-confirm-button"
  }
})
```

If you do not have an accessibility id to reference it is best to describe elements by text, adding [additional attributes](touch-interactions.md#targeting-elements) as necessary.

## Timeouts

All interactions that target an element will wait up to 30 seconds to find the element. If the element is not found, it will throw an error.

## Methods

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

Plays a swipe gesture at the coordinate or specified element

#### By coordinates

Coordinates can be specified in either `px` or `%` (of screen).

<pre class="language-javascript"><code class="lang-javascript"><strong>// swipe up at middle of the screen
</strong><strong>session.swipe({
</strong>    x: '50%',
    y: '50%',
    gesture: 'up', // or 'left', 'down', 'right'
    duration: 1000 // optional, in ms
})
</code></pre>

#### By element

When an element is targeted, `%` values will correlate to the height/width of the element rather than the screen.

```javascript
// swipe left from the middle of an image
session.swipe({
    x: '50%',
    y: '50%',
    element: { accessibilityIdentifier: 'my-image' },
    gesture: 'left'
})
```

#### Complex Gestures

If you have a more complex gesture you can build one by providing a function to the `gesture` argument.

```javascript
// swipe left 100px and then up 100px (L shape)
session.swipe({
    x: '50%',
    y: '50%',
    gesture: g => g.move(-100, 0).move(0, -100)
})

// swipe up-right 25% of the screen
session.swipe({
    x: '50%',
    y: '50%',
    gesture: g => g.move('25%', '-25%')
})

// swipe across an element starting from the middle-left
session.swipe({
    x: '0%',
    y: '50%',
    element: { accessibilityIdentifier: 'my-image' },
    // 100% = width of the targeted element
    gesture: g => g.move('100%', 0)
})
```

The `move` function takes `x, y` arguments and defines the points in the path of your gesture. Each chained `move()` is relative to the previous point.

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
