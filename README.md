# Email Automation Notification System

An automated email notification system built using **n8n, Google Sheets, and Gmail**.

The workflow checks records in a Google Sheet at scheduled intervals. When a record has a **Pending** status, the system automatically sends an email and updates the status to **Sent**. This prevents the same notification from being sent repeatedly.

## Features

* Scheduled workflow execution using n8n
* Reads notification records from Google Sheets
* Checks record status using an IF condition
* Sends emails automatically through Gmail
* Updates the record from `Pending` to `Sent`
* Prevents duplicate email notifications
* Uses dynamic email addresses and message content from Google Sheets

## Technologies Used

* n8n
* Google Sheets
* Gmail
* OAuth 2.0
* Workflow Automation

## Workflow

```text
Schedule Trigger
       ↓
Google Sheets
(Get rows)
       ↓
IF Node
(Status = Pending?)
       ↓
      YES
       ↓
Gmail
(Send Email)
       ↓
Google Sheets
(Update Status → Sent)
```

If the status is not `Pending`, the workflow does not send an email.

## Google Sheet Structure

The workflow uses information stored in Google Sheets such as:

| Field   | Description             |
| ------- | ----------------------- |
| Name    | Name of the recipient   |
| Email   | Recipient email address |
| Message | Notification message    |
| Status  | Notification status     |

Example:

| Name    | Email                                         | Message                   | Status  |
| ------- | --------------------------------------------- | ------------------------- | ------- |
| Student | [example@gmail.com](mailto:example@gmail.com) | Your notification message | Pending |

After successful email delivery:

```text
Pending → Sent
```

## How It Works

1. The **Schedule Trigger** starts the workflow at a configured interval.
2. **Google Sheets** retrieves the notification records.
3. The **IF Node** checks whether the record status is `Pending`.
4. If the status is `Pending`, the workflow continues to the Gmail node.
5. **Gmail** sends the email using the recipient and message from the Google Sheet.
6. **Google Sheets** updates the status to `Sent`.
7. Records already marked as `Sent` do not trigger another email.

## Duplicate Notification Prevention

The system uses the `Status` field to prevent duplicate notifications.

```text
Status = Pending
        ↓
    Send Email
        ↓
Status = Sent
```

When the workflow runs again, records with `Sent` status are ignored.

## Project Structure

```text
email-automation-system/
│
├── workflow/
│   └── email-automation-workflow.json
│
├── screenshots/
│
└── README.md
```

## Learning Outcomes

Through this project, I practiced:

* Workflow automation with n8n
* Google Sheets integration
* Gmail integration
* Conditional logic using IF nodes
* Dynamic data mapping
* Scheduled automation
* Updating records automatically
* Preventing duplicate processing
* OAuth-based application integration
* Git and GitHub project management

## Future Improvements

* Add multiple notification types
* Add email templates
* Add error handling and retry logic
* Add notification history
* Add additional conditions and filters
* Add a dashboard for notification tracking

## Author

**Aravind Amaragonda**

B.Tech – Electronics and Communication Engineering

Aspiring Software Developer
