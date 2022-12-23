# Direct file uploads

[Create new app](create-new-app.md) and [Update existing app](update-existing-app.md) require that you first upload your app to a publicly accessible website URL, from which we then retrieve your app.

If you would prefer to directly upload the app as part of the API call, our endpoints also accept multipart/form-data requests.

You may use the field name `file` to send a direct upload from the local filesystem, rather than using the field `url`. All other field names are identical. To delete a field, set it to an empty string.

The `appPermissions` field is an object in the JSON API. For direct uploads, you should specify the fields as "appPermissions.run", "appPermissions.networkProxy", etc.

```bash
# uploading a new app
curl --http1.1 https://APITOKEN@api.appetize.io/v1/apps -F "file=@file_to_upload.zip" -F "platform=ios"

# updating an existing app
curl --http1.1 https://APITOKEN@api.appetize.io/v1/apps/PUBLICKEY -F "file=@file_to_upload.zip" -F "platform=ios"

# specifying appPermissions
curl --http1.1 https://APITOKEN@api.appetize.io/v1/apps -F "file=@file_to_upload.zip" -F "platform=ios" -F "appPermissions.run=public"
```
