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
2. Add credentials: Google Drive, Google Sheets, Anthropic API
3. Create Google Drive folder structure:

## Documentation

- [Full Technical Writeup](https://docs.google.com/document/d/1Ze5kZyeNIPWqFIl0eoJ1bzSBZjiv7z3S6H1qseAHy5k/edit?tab=t.0) — system design, scoring methodology, edge cases, and hiring insights
