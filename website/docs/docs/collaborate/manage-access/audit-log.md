---
title: "The audit log for dbt Cloud Enterprise"
id: audit-log
description: "You can troubleshoot possible issues and provide security audits by reviewing event activity in your organization."
sidebar_label: "Audit log"
---

To review actions performed by people in your organization, dbt provides logs of audited user and system events in real time. The audit log appears as events happen and includes details such as who performed the action, what the action was, and when it was performed. You can use these details to troubleshoot access issues, perform security audits, or analyze specific events. 

You must be an **Account Admin** to access the audit log and this feature is only available on Enterprise plans.

The dbt Cloud audit log stores all the events that occurred in your organization in real-time, including:

- For events within 90 days, the dbt Cloud audit log has a selectable date range that lists events triggered.
- For events beyond 90 days, **Account Admins** can [export all events](#exporting-logs) by using **Export All**.

## Accessing the audit log

To access audit log, click the gear icon in the top right, then click **Audit Log**.

<div style={{maxWidth: '150px'}}>

<Lightbox src="/img/docs/dbt-cloud/dbt-cloud-enterprise/audit-log-menu.png" title="Audit log menu"/>

</div>

## Understanding the audit log

On the audit log page, you will see a list of various events and their associated event data. Each of these events show the following information in dbt:

* **Event name**: Action that was triggered
* **Agent**: User who triggered that action/event
* **Timestamp**: Local timestamp of when the event occurred

### Event details

Click the event card to see the details about the activity that triggered the event. This view provides important details, including when it happened and what type of event was triggered. For example, if someone changes the settings for a job, you can use the event details to see which job was changed (type of event: `v1.events.job_definition.Changed`), by whom (person who triggered the event: `actor`), and when (time it was triggered: `created_at_utc`). For types of events and their descriptions, see [Events in audit log](#events-in-audit-log).

The event details provides the key factors of an event:

| Name                 | Description                                   |
| -------------------- | --------------------------------------------- |
| account_id           | Account ID of where the event occurred        |
| actor                | Actor that carried out the event - User or Service    |
| actor_id             | Unique ID of the actor                        |
| actor_ip             | IP address of the actor                       |
| actor_name           | Identifying name of the actor                 |
| created_at_utc       | UTC timestamp on when the event occurred      |
| event_type           | Unique key identifying the event              |
| id                   | Unique ID of the event                        |
| service              | Service that carried out the action           |
| source               | Source of the event - dbt Cloud UI or API     |
| v1.events.event_type | This key will be different for each event and will match the event_type. This data will include all the details about the object(s) that was changed. |

## Audit log events

The audit log supports various events for different objects in dbt Cloud. You will find events for authentication, environment, jobs, service tokens, groups, user, project, permissions, license, connection, repository, and credentials.

### Authentication

| Event Name                 | Event Type                               | Description                                            |
| -------------------------- | ---------------------------------------- | ------------------------------------------------------ |
| Auth Provider Changed      | v1.events.auth_provider.Changed          | Authentication provider settings changed               |
| Credential Login Failed    | v1.events.auth.CredentialsLoginFailed    | User login via username and password failed            |
| Credential Login Succeeded | v1.events.auth.CredentialsLoginSucceeded | User successfully logged in with username and password |
| SSO Login Failed           | v1.events.auth.SsoLoginFailed            | User login via SSO failed                              |
| SSO Login Succeeded        | v1.events.auth.SsoLoginSucceeded         | User successfully logged in via SSO  

### Environment

| Event Name          | Event Type                    | Description                          |
| ------------------- | ----------------------------- | ------------------------------------ |
| Environment Added   | v1.events.environment.Added   | New environment successfully created |
| Environment Changed | v1.events.environment.Changed | Environment settings changed         |
| Environment Removed | v1.events.environment.Removed | Environment successfully removed     |

### Jobs

| Event Name  | Event Type                        | Description                  |
| ----------- | --------------------------------- | ---------------------------- |
| Job Added   | v1.events.job_definition.Added   | New Job successfully created |
| Job Changed | v1.events.job_definition.Changed | Job settings changed         |
| Job Removed | v1.events.job_definition.Removed | Job definition removed       |

### Service Token

| Event Name            | Event Type                       | Description                                |
| --------------------- | -------------------------------- | ------------------------------------------ |
| Service Token Created | v1.events.service_token.Created | New Service Token was successfully created |
| Service Token Revoked | v1.events.service_token.Revoked | Service Token was revoked                  |

### Group

| Event Name    | Event Type                    | Description                    |
| ------------- | ----------------------------- | ------------------------------ |
| Group Added   | v1.events.user_group.Added   | New Group successfully created |
| Group Changed | v1.events.user_group.Changed | Group settings changed         |
| Group Removed | v1.events.user_group.Changed | Group successfully removed     |

### User

| Event Name                   | Event Type                          | Description                                     |
| ---------------------------- | ----------------------------------- | ----------------------------------------------- |
| Invite Added                 | v1.events.invite.Added              | User invitation added and sent to the user      |
| Invite Redeemed              | v1.events.invite.Redeemed           | User redeemed invitation                        |
| User Added to Account        | v1.events.account.UserAdded         | New user added to the account                   |
| User Added to Group          | v1.events.user_group_user.Added     | An existing user is added to a group            |
| User Removed from Account    | v1.events.account.UserRemoved       | User removed from the account
| User Removed from Group      | v1.events.user_group_user.Removed   | An existing user is removed from a group        |
| Verification Email Confirmed | v1.events.user.jit.email.Confirmed  | Email verification confirmed by user            |
| Verification Email Sent      | v1.events.user.jit.email.Sent       | Email verification sent to user created via JIT |

### Project

| Event Name      | Event Type                | Description              |
| --------------- | ------------------------- | ------------------------ |
| Project Added   | v1.events.project.Added   | New project added        |
| Project Changed | v1.events.project.Changed | Project settings changed |
| Project Removed | v1.events.project.Removed | Project is removed       |

### Permissions

| Event Name              | Event Type                   | Description                    |
| ----------------------- | ---------------------------- | ------------------------------ |
| User Permission Added   | v1.events.permission.Added   | New user permissions are added |
| User Permission Removed | v1.events.permission.Removed | User permissions are removed   |

### License

| Event Name              | Event Type                     | Description                               |
| ----------------------- | ------------------------------ | ----------------------------------------- |
| License Mapping Added   | v1.events.license\_map.Added   | New user license mapping is added         |
| License Mapping Changed | v1.events.license\_map.Changed | User license mapping settings are changed |
| License Mapping Removed | v1.events.license\_map.Removed | User license mapping is removed           |

### Connection

| Event Name         | Event Type                   | Description                                |
| ------------------ | ---------------------------- | ------------------------------------------ |
| Connection Added   | v1.events.connection.Added   | New Data Warehouse connection added        |
| Connection Changed | v1.events.connection.Changed | Data Warehouse Connection settings changed |
| Connection Removed | v1.events.connection.Removed | Data Warehouse connection removed          |

### Repository

| Event Name         | Event Type                   | Description                 |
| ------------------ | ---------------------------- | --------------------------- |
| Repository Added   | v1.events.repository.Added   | New repository added        |
| Repository Changed | v1.events.repository.Changed | Repository settings changed |
| Repository Removed | v1.events.repository.Removed | Repository removed          |

### Credentials

| Event Name                       | Event Type                    | Description                      |
| -------------------------------- | ----------------------------- | -------------------------------- |
| Credentials Added to Project     | v1.events.credentials.Added   | Project credentials added        |
| Credentials Changed in Project   | v1.events.credentials.Changed | Credentials changed in project   |
| Credentials Removed from Project | v1.events.credentials.Removed | Credentials removed from project |

## Searching the audit log

You can search the audit log to find a specific event or actor, which is limited to the ones listed in [Events in audit log](#events-in-audit-log). The audit log successfully lists historical events spanning the last 90 days. You can search for an actor or event using the search bar, and then narrow your results using the time window.

<div style={{maxWidth: '600px'}}>

<Lightbox src="/img/docs/dbt-cloud/dbt-cloud-enterprise/audit-log-search.png" title="Use search bar to find content in the audit log"/>

</div>

## Exporting logs

You can use the audit log to export all historical audit results for security, compliance, and analysis purposes:

- For events within 90 days &mdash; dbt Cloud will automatically display the 90 days selectable date range. Select **Export Selection** to download a CSV file of all the events that occurred in your organization within 90 days.
- For events beyond 90 days &mdash; Select **Export All**. The Account Admin will receive an email link to download a CSV file of all the events that occurred in your organization.

<Lightbox src="/img/docs/dbt-cloud/dbt-cloud-enterprise/audit-log-section.jpg" title="View audit log export options"/>


