---
description: >-
  Organize your apps effortlessly with Appetize's App Dashboard and Groups,
  enabling seamless app management and access.
---

# Listing Apps

{% hint style="info" %}
For our Enterprise customers we also provide [Custom Launch Pages](../features/custom-launch-pages.md). They can provide a simple bookmark-friendly page for your teams, only showing the applications they are interested in.
{% endhint %}

## Single Applications

### With App Dashboard

The [App Dashboard](https://appetize.io/apps) on Appetize provides you with an overview of all your uploaded apps.

<figure><img src="../.gitbook/assets/image (4).png" alt="" width="563"><figcaption><p>App Dashboard</p></figcaption></figure>

From there, you can:

* **Search** by application name.
* **Filter** your applications by Device Type (Android or iOS) and by enabled/disabled applications.
* **Add notes** to an application for easy identification and organization
* Navigate to the **Manage** page for a specific application, where you can edit settings such as permissions and upload newer builds.
* **Launch and debug** your preferred application.
* **Delete** applications that you no longer need.

### With Rest API

Appetize also supports retrieving a list of your uploaded apps (or a single app by [**publicKey**](sharing-apps.md#public-key)) by making use of our [REST API](broken-reference/):

{% hint style="info" %}
Each uploaded app has a uniquely assigned [**publicKey**](sharing-apps.md#public-key), and looks like this:

```
https://appetize.io/app/:publicKey
```

and can also be seen on the [App Dashboard](https://appetize.io/apps).
{% endhint %}

{% content-ref url="../rest-api/list-apps.md" %}
[list-apps.md](../rest-api/list-apps.md)
{% endcontent-ref %}

## Grouped Applications

Appetize also supports grouping multiple applications that you would like to install simultaneously on the same device.

{% hint style="warning" %}
Simultaneous installation of applications with the same `bundle ID` or `package name` is not possible due to conflict in identifiers.
{% endhint %}

You can view all your App Groups on the [App Group Dashboard](https://appetize.io/app-groups).

### Creating a new group

To create a new group, select the `Add new group` button

<figure><img src="../.gitbook/assets/image (2) (1).png" alt="" width="277"><figcaption><p>Add new group Action</p></figcaption></figure>

A new group will be created with no applications attached

<figure><img src="../.gitbook/assets/image (3) (1).png" alt="" width="453"><figcaption><p>New Group</p></figcaption></figure>

#### Add/Remove Applications

To add applications to the group, select the `add group` action and add all the [**publicKeys**](sharing-apps.md#public-key) for the applications that you want to add to this group

{% hint style="info" %}
Each uploaded app has a uniquely assigned [**publicKey**](sharing-apps.md#public-key), and looks like this:

```
https://appetize.io/app/:publicKey
```

and can also be seen on the [App Dashboard](https://appetize.io/apps).
{% endhint %}

<figure><img src="../.gitbook/assets/image (10) (1) (1) (1) (1) (1) (1).png" alt="" width="455"><figcaption><p>Add a group by publicKey</p></figcaption></figure>

Once you have added all the applications to the group, you can use the group in the same way that you would have used the individual applications (e.g. view, embed etc.).

<figure><img src="../.gitbook/assets/image (5) (1).png" alt="" width="431"><figcaption><p>Example App Group</p></figcaption></figure>

You can also remove individual applications from the group that you no longer want to include by selecting the `remove` action next to the application under the group.
