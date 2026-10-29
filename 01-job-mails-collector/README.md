# 01 Job mails collector

## Problem
Job alert mails from a job board arrive several times a day. Reading them and copying the relevant jobs by hand costs time and is easy to forget.

## Solution
An n8n workflow watches a mailbox over IMAP and only picks up mails from the job board's sender address. A Code node turns the HTML mail into readable text (keeping the links), repairs broken character encoding and writes one Markdown file per mail into an inbox folder. Files I have already reviewed are moved by hand into a subfolder, nothing is deleted.

## Nodes
1. **Email Trigger (IMAP)**: unread mails from one sender, marked as read after processing
2. **Code**: HTML to text, encoding repair, file name from time, source and subject
3. **Read/Write Files from Disk**: writes the Markdown file

## Result
Every new alert is saved as `YYYY-MM-DD_HHMMSS_source_subject.md` in an inbox folder and can be reviewed in one place.

## Notes
- Credentials (mailbox login) are not included in `job-mails-collector.json`. Connect your own IMAP account.
- File access is restricted to the inbox folder with the environment variable `N8N_RESTRICT_FILE_ACCESS_TO`.
- Mails from some sources contain only a link, not the job text. Those are skipped from the filter.
