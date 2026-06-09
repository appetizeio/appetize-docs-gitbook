# Direct file uploads

The[ Create New App](create-new-app.md) and [Update Existing App](update-existing-app.md) endpoints require your app to be hosted at a **publicly accessible URL**.

If you prefer, you can upload the app **directly** as part of the API request using a `multipart/form-data` request.

### 🧾 Notes

* Use the field **`file`** to upload from your local file-system instead of the **`url`** field.
* All other field names stay the same.
* To **delete a field**, pass an **empty string** (e.g., `-F "field="`).
* `appPermissions` (normally a nested object in JSON) should be flattened:
  * e.g., `appPermissions.run`, `appPermissions.networkProxy`, etc.

### 📦 Examples

{% tabs %}
{% tab title="Upload New App" %}
```bash
curl -X POST https://api.appetize.io/v1/apps \
  -H "X-API-KEY: your_api_token" \
  -F "file=@file_to_upload.zip" \
  -F "platform=ios"
```
{% endtab %}

{% tab title="Update Existing App" %}
```bash
curl -X POST https://api.appetize.io/v1/apps/PUBLICKEY \
  -H "X-API-KEY: your_api_token" \
  -F "file=@file_to_upload.zip" \
  -F "platform=ios"
```
{% endtab %}

{% tab title="Specifying App Permissions" %}
```bash
curl -X POST https://api.appetize.io/v1/apps \
  -H "X-API-KEY: your_api_key_here" \
  -F "file=@file_to_upload.zip" \
  -F "platform=ios" \
  -F "appPermissions.run=public"
```
{% endtab %}
{% endtabs %}
