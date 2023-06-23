# Notification

## Introduction

ROQ's notification system allows you to reach your users or user groups through various channels:

- In-app notifications: These are loaded in real time, using a socket connection directly from your web app.
- SMS or push messages: Send notifications directly to your users' mobile phones.
- Traditional e-mails: Deliver messages straight to the users' inbox.

Users have the ability to customize their preferences for each type of notification. For example, they can choose to receive alerts through push messages while getting product updates via e-mail.

## How to Add a New Notification

Establishing effective notifications is a crucial aspect of any successful software application. Notifications engage users and keep them informed about important updates, events, or required actions. With the ROQ platform, you can add a new notification to your project through a straightforward process.

This guide will walk you through the steps needed to add a new notification to your project using ROQ's intuitive interface and powerful features.

### Selecting the Project

Begin by selecting the specific project and environment on the [ROQ Console](https://console.roq.tech/) for which you want to create a new notification. Make sure to choose the appropriate **project** and **environment** before proceeding.

![select-project-and-env](/images/select-project-and-env.png)

### Accessing the Notifications Settings Page

To access the notifications settings page in the ROQ console, click the Notifications menu (represented by a bell icon). On this page, you will see a list of notification templates for the current project.

![roq-console-notification-setting](/images/project-notification-setting.png)

### Creating a New Notification Template

To create a new notification template, click the **Templates** menu, then locate and click the **Create Template** button. This action will initiate the process of creating a new notification template, enabling you to customize the notification according to your project's needs.

![create-notification-template](/images/create-notifications-template.png)

When creating a new notification template, you need to fill in two fields:

1. **Key**: Each template requires a unique key, which will be used as a reference to trigger notifications using the API or programmatically.
2. **Notification Description**: This is where you provide a description of the notification.

After creating a notification template, you will need to configure and activate the channels. Currently, we support three channels: Web (In-App), Email, and SMS.

![configure-template](/images/configure-template.png)

Each of these channels allows you to configure message templates.

![configure-messages](/images/configure-messages-on-channel.png)

Please note that for the **Email** and **SMS** channels to work, you need to set up ROQ with third-party services first in the [Integration]().

After **Create Localized Content** for any channels that you need, the notification will show up on **Notifications Preferences** in your SaaS project.

![saas-notificatons-preferences](/images/notification-settings.png)

