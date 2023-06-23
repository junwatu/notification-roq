# Notification

## Introduction

ROQ's notification system allows you to reach your users or user groups through various channels:

- In-app notifications: These are loaded in real-time, using a socket connection directly from your web app.
- Traditional e-mails: Deliver messages straight to the users' inbox.
- SMS or push messages: Send notifications directly to your users' mobile phones.

Users can customize their preferences for each type of notification. For example, they can choose to receive alerts through push messages while getting product updates via e-mail or SMS.

## How to Add a New Notification

Establishing effective notifications is a crucial aspect of any successful software application. Notifications engage users and keep them informed about important updates, events, or required actions. With the ROQ platform, you can add a new notification to your project through a straightforward process.

This guide will walk you through the steps needed to add a new notification to your project using ROQ's intuitive interface and powerful features.

### Selecting the Project

Begin by selecting the specific project and environment on the [ROQ Console](https://console.roq.tech/) for which you want to create a new notification. Make sure to choose the appropriate **project** and **environment** before proceeding.

![select-project-and-env](/images/select-project-and-env.png)

> You need 

### Accessing the Notifications Settings Page

To access the notifications settings page in the ROQ console, click the Notifications menu (represented by a bell icon). On this page, you will see a list of notification templates for the current project.

![roq-console-notification-setting](/images/project-notification-setting.png)

### Creating a New Notification Template

To create a new notification template, click the **Templates** menu, then locate and click the **Create Template** button. This action will initiate the process of creating a new notification template, enabling you to customize the notification according to your project's needs.

![create-notification-template](/images/create-notifications-template.png)

When creating a new notification template, you need to fill in two fields:

1. **Key**: Each template requires a unique key, which will be used as a reference to trigger notifications using the API or programmatically.
2. **Notification Description**: This is where you describe the notification.

After creating a notification template, you will need to configure and activate the channels. Currently, we support three channels: Web (In-App), Email, and SMS.

![configure-template](/images/configure-template.png)

Each of these channels allows you to configure message templates.

![configure-messages](/images/configure-messages-on-channel.png)

Please note that for the **Email** and **SMS** channels to work, you need to set up ROQ with third-party services first in the [Integration]() ROQ Console.

To create localized content for the channel messages, click **Create Localized Content** button. Fill in the fields to your needs and save it.

![create-localized-content](/images/cretae-localized-content.png)

The localized content supports custom variables, enabling you to notify users with custom values in the message.

![localized-content-with-vars](/images/localized-content-with-vars.png)

You can set the `downloadLink` variable with Notification API or by query via GraphQL API.

After **Create Localized Content** for any channels that you need, the notification will show up on **Notifications Preferences** in your SaaS project.

![saas-notificatons-preferences](/images/notification-settings.png)

### Test Notifications

To test the notifications we created earlier we need to query data from the GraphQL server. The URL for  this GraphQL server is in **Project Details** in the ROQ console.

This page shows all the credentials to access the GraphQL server.

![](/images/project-details-graphql-api-url.png)

To test or trigger the notifications, we can use a GraphQL query like this:

```graphql
mutation {
  notify(
    notification: {
      key: "translated-file-conversion"
      recipients: {
        userIds: ["163ae909-b611-423c-b105-67f86a8870ac"]
        userGroups: { operator: AND, userGroupIds: ["325a3bc5-3d65-4868-b4af-85d4f8f206b8"] }
        allUsers: false
      },
      data: [{ key: 'downloadLink', value: 'https://roq.ai' }]
    }
  ) {
    usersNotified {
      count
    }
  }
}
```

If you execute the GraphQL query above in the GraphQL API server sandbox, you will get 1 user notified.

![graphql-query-sandbox](/images/graphql-queries.png)

and the triggered notifications will show to any recipients.

![triggered-notification](/images/triggered-notification.png)

## Notifications API

ROQ's notifications enable you to notify your users or user groups on various channels.

To notify your users you can use the `notify()` API. It's important to use the same key which you set to the notification template.

### Mutations

`notify()`

The `notify()` mutation enables you to notify:

- A single user or multiple users
- Users of one or multiple user groups
- All of your users.

You can find the full API doc of this mutation [here](https://mars-pp.roq-platform.com/docs/#mutation-notify)

The API requires a `key` parameter that you need to configure in ROQ Console, see instructions [here](). The notified users are defined in the recipients variable as shown below.

**GraphQL**

```graphql
mutation {
  notify(
    notification: {
      key: "aaa"
      recipients: {
        userIds: ["abc123"]
        userGroups: { operator: AND, userGroupIds: ["xyz789"] }
        excludedUserIds: ["abc123"]
        allUsers: false
      }
      data: [{ key: "xyz789", value: "xyz789" }]
    }
  ) {
    usersNotified {
      count
    }
  }
}
```

**Node.js SDK**

```js
await client.asSuperAdmin().notify({
  notification: {
    key: 'aaa',
    recipients: {
      userIds: ['abc123'],
      userGroups: { operator: 'AND', userGroupIds: ['xyz789'] },
      excludedUserIds: ['abc123'],
      allUsers: false,
    },
    data: [{ key: 'xyz789', value: 'xyz789' }],
  },
});
```

| Parameter               | Type    | Description |
|-------------------------|---------|-------------|
| key                     | string  | Key of notification-type that you created in the Console, eg."WELCOME_NOTIFICATION" |
| recipients:userIds      | array   | Array of user IDs that are notified. |
| recipients:userGroups   | object  | An object that represents a list of user groups and an operator which can be set to "AND"(intersection of users) and "OR" (union of users). |
| recipients:excludedUserIds | array   | List of user IDs (of ROQ Platform) who shouldn't be notified. A typical use case is when a user performs an action and all users of the same user group should be notified, except for the acting user |
| recipients:allUsers     | bool    | If set to true then all users will be notified. |
| data                    | array   | List of key/value pairs that you can use in the content section of the Notification template |

### Queries

`notifications()`

We can fetch notifications by using the `notifications()` query. You can find the full API doc of this query [here](opens in a new tab).

**GraphQL**

```graphql
query {
  notifications(page: 0, seen: false) {
    data {
      id
      title
      content
      icon
      seen
      read
    }
  }
}
```

**Node.js SDK**

```js
await client.asSuperAdmin().notifications();
```
