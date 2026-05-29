# Setup Guide

Complete every step below before running the workflow. Missing credentials are the most common cause of failure.

## 1. Google Form

1. Go to [forms.google.com](https://forms.google.com) and create a new blank form
2. Set the title to: `Job Application`
3. Add the following fields:
   - Short answer: Full Name (required)
   - Short answer: Email Address (required)
   - Short answer: Role Applying For (required)
   - Short answer: Years of Experience (required)
   - File upload: Upload Your CV (required) — allow PDF and DOC only
4. Go to Settings > Responses > enable Collect email addresses
5. In the Responses tab, click the Sheets icon to link a Google Sheet — you will need this sheet's URL in n8n

## 2. Google OAuth (for n8n to access Drive)

1. Go to [console.cloud.google.com](https://console.cloud.google.com) and create a new project called `n8n-cv-screener`
2. Enable the following APIs: Google Drive API, Google Sheets API
3. Go to APIs & Services > Credentials > Create Credentials > OAuth 2.0 Client ID
4. Application type: Web application
5. Add this as an authorised redirect URI: `http://localhost:5678/rest/oauth2-credential/callback`
6. Download the JSON and copy the Client ID and Client Secret
7. In n8n: Settings > Credentials > New > Google Drive OAuth2 > paste Client ID and Secret > Connect

## 3. Gemini API Key

1. Go to [aistudio.google.com](https://aistudio.google.com)
2. Click Get API Key > Create API Key in new project
3. Copy the key — it starts with `AIza`
4. Paste it as the value of the `x-goog-api-key` header in the Gemini HTTP Request node

## 4. Notion Integration

1. Go to [notion.so/my-integrations](https://www.notion.so/my-integrations) and create a new integration
2. Name it `cv-screener`, select your workspace, and copy the Internal Integration Token (starts with `ntn_`)
3. Create a new database in Notion using the schema defined in [notion/database_schema.md](../notion/database_schema.md)
4. Open the database > click the three-dot menu > Connections > connect your integration
5. Copy the Database ID from the database URL: `notion.so/workspace/{DATABASE_ID}?v=...`
6. In n8n, paste the token as a Bearer token in the Notion HTTP Request node Authorization header

## 5. Email (Gmail/SMTP)

1. In n8n, go to Settings > Credentials > New > Gmail OAuth2 (or SMTP)
2. Connect your Google account or enter your SMTP credentials
3. The hiring manager's email address is set directly inside the email node in the workflow

## Credentials Summary

| Credential | Where It Goes |
|------------|---------------|
| Google OAuth Client ID + Secret | Google Drive credential in n8n Settings |
| Gemini API Key (`AIza...`) | HTTP Request header: `x-goog-api-key` |
| Notion Token (`ntn_...`) | HTTP Request Authorization Bearer header |
| Notion Database ID | HTTP Request URL path |
| Hiring Manager Email | Email node in the workflow |
