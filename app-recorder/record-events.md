# Record events

When app recording is enabled, the Appetize.io iFrame will post `recordedEvent` messages to its parent window. See [Cross-document messages](../core-features/cross-document-messages.md) for more information on how this works. The message will be an object with `type` set to `recordedEvent`. Its `value` field will be an event object with the following fields:

* `type` - what happened, e.g. "keypress", "click", "swipe", "scrollToElement"
* `id` - a string that identifies this event \(unique per recording\)
* `element` - an object representation of the UI element that the event targeted. It will have fields:
  * `path` - the element's position in the UI hierarchy
  * `class` - the class of the element
  * `text` - \(Android\) text displayed
  * `resource-id` - \(Android\) the resource id corresponding to the element
  * `content-desc` - \(Android\) the content description used for accessibility
  * `windowType` - \(Android\) the type of window \(application/system/input-method\)
  * `label` - \(iOS\) text displayed
  * `accessibilityId` - \(iOS\) identifier used for accessibility
  * `parentClass` - \(iOS\) parent class of the element
* `time` - when the event occurred, in seconds since session start
* `ui` - an xml representation of the app's entire UI when the event occurred
* `xPos` - the x position \(from left\) of where a tap event occurred
* `yPos` - the y position \(from top\) of where a tap event occurred

Note that the event object is a simple javascript object that can be serialized to JSON and stored for later use.

The iFrame may also post `deleteEvent` messages, formatted the same way. It is used, for example, when a set of previous swipes should be replaced with a "scrollToElement" event. When receiving a `deleteEvent` message, use the `id` of the event search backwards in the recording to find the event that should be deleted.

