# Google Forms → Sheets Email Reminder (Apps Script)

A lightweight task reminder system built with **Google Forms, Google Sheets, and Google Apps Script**.  
Users submit tasks via Google Forms and automatically receive **HTML email reminders** at scheduled times, with support for **advance reminders, recurring tasks, and completion tracking**.

---

## ✨ Features

- Task submission via Google Forms
- Automated email reminders using Google Apps Script
- Reminder options:
  - At scheduled time
  - 10 / 30 minutes before
  - 1 hour before
  - 1 day before (custom time)
- Recurring reminders:
  - Weekly
  - Monthly
  - Yearly
- Automatic Sunday handling (shift to Monday)
- Duplicate-send prevention using:
  - Status column
  - `LockService`
- Stop reminders by marking tasks as **Completed**
- Responsive **HTML email template**
- Built-in debugging helper

---

## 🧱 Architecture

Google Form
↓
Google Sheet (Form Responses)
↓
Google Apps Script (Time-driven trigger)
↓
HTML Email Reminder

yaml
Sao chép mã

---

## 📄 Google Sheet Requirements

The response sheet must contain columns whose headers include the following keywords  
(case-insensitive, partial matches are supported):

| Purpose | Required keyword in column header |
|------|----------------------------------|
| Task title | `task name` |
| Task description | `description` |
| Event date | `event date` |
| Event time | `event time` |
| Main recipient email | `email` |
| Additional emails (optional) | `additional email` |
| Reminder option | `remind` |
| Recurrence option (optional) | `recurring` |
| Send status | `status` |
| Completion flag (optional) | `completed` |

> Header numbering (e.g. `3/ Event Date`) is supported.

---

## ⚙️ Setup Instructions

### 1️⃣ Create a Google Form
Create a Google Form with:
- Text inputs for task name and description
- Date picker for event date
- Time picker for event time
- Multiple-choice question for reminder options
- Optional multiple-choice question for recurrence

Link the form to a Google Sheet.

---

### 2️⃣ Add Apps Script
1. Open the linked Google Sheet  
2. Extensions → Apps Script  
3. Paste the script into `Code.gs`  
4. Save

---

### 3️⃣ Add Required Columns
Manually add the following columns to the response sheet:
- **Status**
- **Completed** (checkbox recommended)

---

### 4️⃣ Create a Time-Driven Trigger
In Apps Script:
- Triggers → Add Trigger
- Function: `checkReminders`
- Event source: **Time-driven**
- Frequency: every **1–5 minutes**

---

### 5️⃣ Authorize the Script
Run `checkReminders` once manually to grant permissions.

---

## 🧪 Quick Test

To test immediately:
1. Submit a new form entry
2. Set the event time to **10 minutes in the future**
3. Choose reminder = **10 minutes before**
4. Run `checkReminders` manually

➡️ The reminder email should arrive within seconds.

---

## 🧠 How It Works

- Dates and times are safely parsed from:
  - Native Date objects
  - Google Sheets serial numbers
  - Display strings (AM/PM supported)
- Emails are sent only within a **time window**:
  - `[remindTime, remindTime + 20 minutes]`
- Tasks already marked as:
  - **Sent** → skipped
  - **Completed** → skipped
- Recurring tasks automatically advance to the next cycle

---

## 🛠 Debugging

Use the helper function:
```js
debugRow(rowNumber)
This logs:

Parsed date and time

Column mappings

Reminder option

Completion status

🔒 Reliability & Safety
Uses LockService to prevent concurrent duplicate sends

Escapes all user input in HTML emails

Designed to be idempotent and safe for frequent triggers

🎨 Customization
You can easily customize:

Email HTML template

Reminder time window

Recurrence rules

Column header keywords

Date/time formatting and timezone

📜 License
MIT License
Free to use, modify, and distribute.

🙌 Credits
Built with Google Apps Script
Designed as a reusable automation template for task reminders.
