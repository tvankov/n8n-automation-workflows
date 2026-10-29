# 03 Job feed ETL pipeline

n8n workflow name: *ETL Stellen Pipeline: RSS Feed zu CSV*

## Problem
The public job portal service.bund.de publishes about 500 job ads in one RSS feed. Most of them are irrelevant for a data analyst, the same job often appears twice from different sources, and employer, place and deadline are buried in an HTML text block.

## Solution
A small ETL pipeline that runs every day at 10:00 (Europe/Berlin).

| Step | What happens | Node |
|---|---|---|
| Extract | Read the RSS feed (about 500 items) | RSS Read |
| Transform | Strip HTML, decode characters, extract employer, place and application deadline, remove duplicates (same title and employer), flag matches by keywords in the title and exclude unwanted ones | Code |
| Filter | Keep only the matches | Filter |
| Load | Write the result as a CSV file with the date and time in the file name | Convert to File, Read/Write Files from Disk |

## Result
Every run writes one clean CSV file (`stellen_YYYY-MM-DD_HHmm.csv`) with the columns `titel`, `arbeitgeber`, `ort`, `bewerbungsfrist`, `veroeffentlicht`, `link`, `treffer`. On the first run, 500 items became 484 after removing duplicates and 8 relevant ads after filtering. The file opens directly in Excel or Power BI.

## Notes
- The keyword list and the exclusion list are regular expressions at the top of the Code node and are easy to change.
- Duplicates are detected by title plus employer, because the same ad has different links on different portals.
- The match is based on the title only, so a good ad can be missed if the keyword appears only in the text.
- The file path in the write node is a placeholder (`C:/n8n-data/jobs/`). Set it to a folder on your machine. If you use `N8N_RESTRICT_FILE_ACCESS_TO`, this folder has to be allowed there.
- The workflow is exported as inactive. Activate it after import.
