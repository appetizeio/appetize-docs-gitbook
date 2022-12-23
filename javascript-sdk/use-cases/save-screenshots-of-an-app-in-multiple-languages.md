# Save screenshots of an app in multiple languages

```javascript
const session = await client.startSession()

const languages = ['en', 'fr', 'ge', 'it']

// iterate over each language
for (let i = 0; i < languages.length; i++) {
    const language = languages[i]

    // set the language (this will restart the app!)
    await session.setLanguage(language)

    // take screenshot and upload somewhere
    const screenshot = await session.screenshot()
    await uploadSomewhere(screenshot.data, screenshot.mimeType)
    
    // OR 
    
    // take screenshot and use as src for an img tag
    const screenshot = await session.screenshot('base64')
    const imgElement = document.createElement("img")
    imgElement.src = screenshot.data
    document.body.appendChild(imgElement)
}
```
