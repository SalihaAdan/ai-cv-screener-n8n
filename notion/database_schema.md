# Notion Database Schema

This is the exact database structure required for the workflow to create candidate cards correctly. Property names and types must match exactly — any mismatch will cause a 400 error from the Notion API.

## Database Properties

| Property Name | Notion Type | Description |
|---------------|-------------|-------------|
| Name | Title | Candidate's full name |
| Email | Email | Candidate's email address |
| Role | Rich Text | Role the candidate applied for |
| Years of Experience | Number | Years of experience from the form |
| AI Score | Number | Fit score returned by Gemini (1–10) |
| Strengths | Rich Text | AI-written strengths summary |
| Gaps | Rich Text | AI-written gaps summary |
| Recommendation | Select | Strong Yes / Yes / No |
| Status | Select | To Review / Rejected |
| Applied At | Date | Timestamp of form submission |

## Select Field Options

**Recommendation**
- Strong Yes
- Yes
- No

**Status**
- To Review
- Rejected

## Notes

- The `Name` field must be set as the database title property.
- All property names are case-sensitive — use them exactly as listed above.
- The `Applied At` field expects ISO 8601 format: `2024-01-01T00:00:00Z`
