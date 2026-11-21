# n8n Form Email Validator

An n8n automation that watches a Google Form's response sheet, checks whether each submitted email address is valid, and sends a personalized thank-you email through Gmail only when it is.

## How it works

1. A user fills in the Google Form (name, email, and other fields).
2. Google Forms saves the response to a Google Sheet.
3. The **Google Sheets Trigger** detects the new row (polls every minute).
4. An **If** node checks the email address against a regex.
5. **Valid email:** a **Gmail** node sends a personalized thank-you message.
6. **Invalid email:** nothing is sent.

## Tools used

- [n8n](https://n8n.io) (Cloud)
- Google Forms and Google Sheets
- Gmail

## Setup

1. Create a Google Form with at least **Name** and **Email Address** questions, and link it to a Google Sheet.
2. In n8n, go to **Workflows > Import from file** and choose `form-email-validator.json`.
3. Connect your own credentials:
   - Google Sheets Trigger (Google account)
   - Gmail (Google account)
4. In the Google Sheets Trigger node, select your own spreadsheet and sheet.
5. Make sure the column names in the expressions match your sheet exactly. Column names can contain trailing spaces, for example `Email Address `.
6. Click **Publish** to activate the workflow.

## Email validation

The If node uses this regex:

```
^[^\s@]+@[^\s@]+\.[^\s@]+$
```

This only checks the **format** of the address (no spaces, one `@`, a dot after it). It does **not** confirm that the mailbox exists, so an address like `fakeperson123@gmail.com` passes the check and the email will bounce. For real deliverability checks, add an email verification API or a confirmation link step.

## Possible improvements

- Log invalid emails to a separate Google Sheet tab.
- Add an email verification API (Hunter, ZeroBounce, etc.).
- Add a confirmation link (double opt-in).

## Notes

No credentials or API keys are included in this repository. You must connect your own accounts after importing the workflow.
