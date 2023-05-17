# Playback Action Matching

A central problem when playing back recorded actions is to find the recorded element in the new UI during playback. Apps may differ between recording and playback because of changes to the content, design, device dimensions, or language.

When searching for correct element during playback, we attempt to find a unique match based on the rules listed below. Each rule defines the set of fields we will consider. If there are multiple elements that satisfy a rule, we will attempt to "break the tie" by considering defining characteristics of sibling and parent elements. If multiple matches or no matches remain, we move on to the next rule.

At the end of the matching algorithm, if no matches or multiple matches are found, the Javascript SDK will return an error.

### On Android, we match using these rules:

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

### On iOS, we match using these rules:

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
