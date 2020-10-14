# Playback events

To playback a recorded event, send a cross-document message with `type` field set to `playEvent`, and `value` set to a `playback` object. We will attempt to locate the element of the recorded event and repeat the action.

A `playback` object should have the fields:

* `event` - the entire event object that was previously recorded
* `timeout` - \(default 10\) the number of seconds to wait for a match of the recorded element
* `strictMatch` - \(default false\) if true, element must match all recorded attributes exactly. Otherwise, we will attempt to find the best matching element
* `id` - \(optional\) a string to identify this playback attempt, to help identify success or failure.

If playback is successful, the iFrame will post a cross-document message with `type` set to `playbackFoundAndSent`. Its `value` field will be an object with the fields:

* `id` - the id string that was optionally provided to `playEvent`
* `playback` - if `id` was not provided, the entire playback object
* `matchedElement` - the element that matched the original recorded event
* `matchedOn` - an array of attributes where the new element matched the recorded element

If the playback failed the iFrame will post a cross-document message with `type` set to `playbackError`. Its `value` field will be an object with the fields:

* `id` - the id string that was optionally provided to `playEvent`
* `playback` - if `id` was not provided, the entire playback object
* `errorId` - a string that may be one of:
  * `notFound` - we timed out waiting for a matching element to appear
  * `uiError` - we were unable to retrieve the UI heirarchy for the app
  * `unknown` - unknown error
* `message` - a string describing the error

### Playback element matching

A central problem when playing back recorded events is to find the recorded element in the new UI during playback. Apps may differ between recording and playback because of changes to the content, design, device dimensions, or language.

When searching for correct element during playback, we attempt to find a unique match based on the rules listed below. Each rule defines the set of fields we will consider. If there are multiple elements that satisfy a rule, we will attempt to "break the tie" by considering defining characteristics of sibling and parent elements. If remain multiple matches or there are no matches, we move on to the next rule.

In scrollable views, the path can be misleading as the exact scroll position may differ between playback and recording. Therefore, path is removed from the rules if the element is inside of a scrollable view. \(Not yet implemented on iOS, see [Known Issues](overview.md#known-issues) above.\)

On Android, we match using these rules:

1. content-desc, text, path, class, resource-id
2. content-desc, path, class, resource-id
3. content-desc
4. text, class, resource-id
5. text, class
6. text
7. path, class, resource-id
8. path, class
9. path, resource-id
10. class, resource-id
11. class

On iOS, we match using these rules:

1. accessibilityIdentifier, text, path, class, baseClass
2. accessibilityIdentifier, text, class, baseClass
3. accessibilityIdentifier, path, class, baseClass
4. accessibilityIdentifier
5. text, path, class, baseClass
6. text, class, baseClass
7. text, class
8. path, class, baseClass
9. path, class
10. path, baseClass
11. class, baseClass
12. class
13. baseClass

