# AI CV Screener with Notion Talent Board

An automated CV screening pipeline built with n8n, Gemini AI, Google Forms, and Notion. Submitted resumes are parsed and evaluated by AI, which scores each candidate and pushes shortlisted profiles into a structured Notion talent board — so hiring decisions are based on data, not whoever got reviewed last.

## What It Does

A candidate fills out a Google Form and uploads their CV (PDF or DOC). The moment they submit, n8n picks up the response, fetches the CV from Google Drive, and sends it to Gemini AI with a scoring prompt built around the job requirements. Gemini returns a fit score from 1 to 10 along with a plain-English breakdown of strengths and gaps. n8n then creates a structured card in a Notion database with all candidate information ready to review. If the score meets the threshold, the hiring manager receives an email alert instantly. Every applicant is logged — no one falls through the cracks.

## Tech Stack

| Tool | Role |
|------|------|
| n8n | Workflow engine — orchestrates every step |
| Google Forms | Applicant intake — name, email, role, CV upload (PDF or DOC) |
| Google Drive | Stores uploaded CV files |
| Gemini 2.5 Flash Preview | AI screening — scores CV and writes summary |
| Notion API | Creates structured candidate cards in a database |
| Gmail/SMTP | Notifies hiring manager for high-scoring candidates |

## Workflow Overview

1. Google Sheets trigger detects a new form submission
2. CV file is fetched from Google Drive
3. A Code node extracts and encodes the CV, and fetches the last row to handle data flow
4. Gemini AI scores the CV against job criteria
5. A Code node parses the AI response into structured fields
6. A Notion card is created for the candidate
7. If score >= 7, an email alert is sent to the hiring manager

## Project Structure

```
ai-cv-screener-notion/
├── workflow/          # Importable n8n workflow JSON
├── notion/            # Notion database schema setup
├── docs/              # Setup guide and architecture breakdown
└── assets/            # Screenshots and demo video
```

## Getting Started

See [docs/setup.md](docs/setup.md) for full credentials and configuration instructions.
