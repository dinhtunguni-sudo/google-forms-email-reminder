# Google Forms → Sheets Email Reminder (Apps Script)

A lightweight reminder system built with Google Forms, Google Sheets, and Google Apps Script.  
Users submit tasks via a Google Form and receive HTML email reminders at scheduled times.

## Features
- Scheduled reminders with a configurable send window
- Reminder offsets (minutes/hours/days before)
- Weekly/monthly/yearly recurrence
- Optional completion flag to stop reminders
- Duplicate-send prevention (status column + LockService)
- HTML email template included

## Setup
1. Create a Google Form and link it to a Google Sheet.
2. Open the Sheet → Extensions → Apps Script.
3. Create two script files: `config.gs` and `main.gs`, then paste the code.
4. Update column numbers in `config.gs` to match your sheet.
5. Create a time-driven trigger for `checkReminders` (every 1–5 minutes).
6. Run `checkReminders` once to authorize.

## Notes
- This repository is 100% English-only source code.
- It uses fixed column indexes rather than header-name matching.

## License
MIT
