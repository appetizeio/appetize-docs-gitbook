---
description: >-
  Session History provides a centralized view of sessions run in your
  organization. Use it to review recent activity, analyze usage, and
  troubleshoot issues.
---

# Session History

You can access [Session History](https://appetize.io/sessions) directly from the application sidebar:

<figure><img src="../.gitbook/assets/image (76).png" alt=""><figcaption><p>Session History in application sidebar</p></figcaption></figure>

***

## **Session List**

<figure><img src="../.gitbook/assets/image (77).png" alt=""><figcaption></figcaption></figure>

The list displays recent sessions with the newest session at the top.

* **Admins** can view all sessions in the organization.
* **Developers and regular users** see only their own sessions.

Each session row provides a quick overview of session context, including who ran it, which app and device were used, when it started, and any available logs or attachments.

### **Filtering Sessions**

Session History includes several filters to help you narrow the list of sessions.

#### **Search**

<figure><img src="../.gitbook/assets/image (78).png" alt=""><figcaption><p>Search Field</p></figcaption></figure>

Use the search field to quickly find sessions by:

* **App ID**
* **App name**
* **Username**

#### **Date Range**

<figure><img src="../.gitbook/assets/image (79).png" alt=""><figcaption><p>Date Range Picker</p></figcaption></figure>

Select a start and end date to focus on sessions from a specific period.\
The range is inclusive and supports selecting any period allowed by the interface.

#### **User**

A dedicated user filter allows you to refine sessions by who ran them.

* **Admins** can select one or multiple users.
* **Developers and regular users** are limited to viewing their own sessions.

#### **Device**

Filter sessions by device type, or choose **All devices** to include everything.

#### **Operating System**

Filter sessions by OS version, or choose **All OS Versions** to include all versions.

### **Exporting Sessions**

An **Export CSV** button allows you to download the sessions that match your current filters.\
The exported file includes all visible columns along with additional session fields that may not appear in the table.

## **Session Details**

<figure><img src="../.gitbook/assets/image (82).png" alt=""><figcaption><p>Session Detail Row</p></figcaption></figure>

Each session row includes key information that helps you understand the context of the session:

* **User information**\
  Shows who initiated the session. This may be the authenticated user’s email, an API token label, or a descriptive label for anonymous sessions.
* **App details**\
  Information about the app, app group, build, or related metadata.
* **Device and OS**\
  The device model and operating system used during the session.
* **Date**\
  When the session took place.&#x20;
* **Queue time**\
  How long the session waited before starting.
* **Duration**\
  How long the session lasted.\
  Ongoing sessions may show **In progress**.
* **Attachments**\
  Icons linking to downloadable logs or other session files. Icons are grayed out if an attachment is not available.
