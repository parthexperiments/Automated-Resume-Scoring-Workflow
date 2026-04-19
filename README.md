# Automated Resume Relevance Scoring Workflow

An n8n workflow that automatically scores candidate resumes against a 
Job Description using Claude AI, outputting structured results to Google Sheets.

## What it does

- Triggers automatically when a PDF resume is uploaded to Google Drive
- Validates the Job Description quality before scoring any resume
- Scores each candidate across 5 weighted dimensions (0–100)
- Writes results to a 3-tab Google Sheet built for HR triage
- Handles 9 edge cases — nothing fails silently

## Scoring dimensions

| Dimension | What it measures | Default weight |
|---|---|---|
| D1 Skills Match | Must-have skills confirmed vs inferred vs missing | 35% |
| D2 Experience | Relevant years and domain match | 25% |
| D3 Seniority | Ownership signals vs required level | 20% |
| D4 Impact Quality | CAR structure and quantified results | 15% |
| D5 Red Flags | Gaps, short tenures, keyword stuffing | 5% |

## Tech stack

- **Workflow**: n8n
- **AI**: Claude Haiku (extraction + triage) + Claude Sonnet (scoring)
- **Storage**: Google Drive + Google Sheets

## Setup

1. Import `workflow/resume_scoring_workflow.json` into n8n
2. Add credentials — the following are required:
   - **Anthropic API key** — for Claude Haiku and Sonnet scoring
   - **Google Drive OAuth** — for reading resumes and JD from Drive
   - **Google Sheets OAuth** — for writing results to the output sheet
3. Create Google Drive folder structure
Hiring Pipeline/
Resumes/
JD/
Output/
4. Fill the config sheet — see docs for field guide
5. Set `Ready_To_Score = YES` and upload resumes

## Optional Integrations

**Slack error notifications** — a Slack node is already wired into the 
workflow on the error path but is currently inactive. To enable it:
1. Add your Slack credentials in n8n
2. Update the channel name in the Slack node (default: `#recruiting`)
3. Activate the node — it will notify your channel whenever a resume 
   fails processing (wrong file type, JD not found, extraction failed etc.)

## Documentation

- [Full Technical Writeup](https://docs.google.com/document/d/1Ze5kZyeNIPWqFIl0eoJ1bzSBZjiv7z3S6H1qseAHy5k/edit?tab=t.0) — system design, scoring methodology, edge cases, and hiring insights
