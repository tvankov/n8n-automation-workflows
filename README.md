# n8n automation workflows

Small n8n workflows I built to automate recurring work: sorting incoming mail, triaging requests and keeping personal data out of downstream steps. Every workflow keeps a human in the loop, nothing is sent automatically.

I am a software developer (15+ years) retraining as a data analyst. These workflows are part of my portfolio next to my Python and Power BI projects: [github.com/tvankov](https://github.com/tvankov).

## Workflows

| # | Workflow | Problem | Result |
|---|---|---|---|
| 01 | [Job mails collector](01-job-mails-collector/) | Job alert mails arrive daily and have to be read and copied by hand | Each alert becomes a clean Markdown file in a folder, ready for review |
| 02 | [Request triage with anonymisation](02-request-triage-anonymisation/) | Contact requests need sorting by type and urgency, and contain personal data | Requests are classified, anonymised, answered with a route and saved with a reply draft |

## How to use the files

Each folder contains the exported workflow (`<folder-name>.json`), a screenshot (`<folder-name>.png`) and a short README. In n8n: **Workflows → Import from file**. Credentials are not part of the export, so you have to connect your own mailbox or webhook settings. The file path in the write node is a placeholder, set it to a folder on your machine.

## Tools

n8n (self-hosted, local), JavaScript in Code nodes, IMAP, webhooks, Markdown output.

## Status and limits

- Both workflows run locally on my machine.
- Workflow 02 is tested with requests sent to the webhook. It is not yet connected to a live website form.
- Reply drafts are suggestions only. A person reads and sends them.
