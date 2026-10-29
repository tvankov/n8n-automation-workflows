# n8n automation workflows

Small n8n workflows I built to automate recurring work: sorting incoming mail, triaging requests, keeping personal data out of downstream steps and cleaning a public data feed (ETL). Every workflow keeps a human in the loop, nothing is sent automatically.

I am a software developer (15+ years) retraining as a data analyst. These workflows are part of my portfolio next to my Python and Power BI projects: [github.com/tvankov](https://github.com/tvankov).

## Workflows

| # | Workflow | Problem | Result |
|---|---|---|---|
| 01 | [Job Mail Sammler: IMAP zu Markdown](01-Job-Mail-Sammler-IMAP-zu-Markdown/) | Job alert mails arrive daily and have to be read and copied by hand | Each alert becomes a clean Markdown file in a folder, ready for review |
| 02 | [Kontaktanfragen einordnen: Webhook zu Antwort](02-Kontaktanfragen-einordnen-Webhook-zu-Antwort/) | Contact requests need sorting by type and urgency, and contain personal data | Requests are classified, anonymised, answered with a route and saved with a reply draft |
| 03 | [ETL Stellen Pipeline: RSS Feed zu CSV](03-ETL-Stellen-Pipeline-RSS-Feed-zu-CSV/) | A public RSS feed has about 500 job ads, with duplicates and key data hidden in HTML text | Extracted, cleaned, deduplicated and filtered to the relevant ads, saved as a CSV file every day |

## How to use the files

Each folder contains the exported workflow (`<folder-name>.json`), a screenshot (`<folder-name>.png`) and a short README. In n8n: **Workflows → Import from file**. Credentials are not part of the export, so you have to connect your own mailbox or webhook settings. The file path in the write node is a placeholder, set it to a folder on your machine.

## Tools

n8n (self-hosted, local), JavaScript in Code nodes, regular expressions, IMAP, webhooks, RSS, Markdown and CSV output.

## Status and limits

- All workflows run locally on my machine, so n8n has to be running for the scheduled ones.
- Workflow 02 is tested with requests sent to the webhook. It is not yet connected to a live website form.
- Reply drafts are suggestions only. A person reads and sends them.
