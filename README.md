NuDesk AI Candidate Referral Automation

An end-to-end recruiting operations workflow that turns an employee referral into structured candidate data, AI-assisted evaluation, automated candidate communication, recruiter notification, and tracker updates.

Built as a technical assessment/demo. Candidate data and CVs included in this repository are synthetic.



What it does

The workflow automates the repetitive steps after an employee submits a referral:

Receives candidate information and a PDF resume from a custom HTML form.

Checks Google Sheets for an existing candidate email to prevent duplicates.

Extracts text from the resume.

Uses Google Gemini to evaluate the candidate against a defined scoring rubric.

Saves structured candidate data and the AI evaluation to Google Sheets.

Sends a confirmation email to the candidate.

Automatically advances candidates scoring 75+ to an assessment.

Notifies the recruiter with the candidate's score, strengths, gaps, and analysis.

Updates the candidate status in the tracker.

Preserves failed CV/AI processing attempts as Processing Error for manual review.

The AI score is used for operational routing, not as a final hiring decision.


Stack

Workflow automation: n8n Cloud

AI: Google Gemini

CV parsing: n8n Extract from File

Tracker: Google Sheets

Email: Gmail

Intake: Custom HTML / JavaScript form

Candidate routing

AI Score

Recommendation

Automatic action

90–100

Strong Fit

Send assessment + notify recruiter

75–89

Good Fit

Send assessment + notify recruiter

60–74

Review

Keep for review

40–59

Weak Fit

Keep for review

0–39

Not Recommended

Keep for review

The scoring prompt awards points only for evidence present in the CV and includes safeguards against instructions embedded inside resume content.


Validation results

The final workflow was tested across multiple candidate profiles:

Candidate

Score

Result

Ethan Carter

97

Strong Fit — assessment sent

Sofia Martinez

72

Review — no automatic advancement

Daniel Brooks

45

Weak Fit — no automatic advancement

Emma Wilson

15

Not Recommended

Michael Turner

8

Not Recommended

Duplicate detection and processing-error handling were also tested separately.

Screenshots

Referral form



Candidate tracker



Recruiter notification



Additional screenshots are available in screenshots/.

Repository structure

.
├── README.md
├── workflow/
│   └── candidate-referral-workflow.json
├── form/
│   └── NuDesk_Employee_Referral_Form.html
├── sample-data/
│   └── sample candidate CVs
└── screenshots/
    └── workflow and demo screenshots

Setup

The repository contains a sanitized version of the workflow. Credentials and live endpoints are intentionally not included.

To run it:

Import workflow/candidate-referral-workflow.json into n8n.

Configure your own Google Gemini, Gmail, and Google Sheets credentials.

Select your candidate-tracker spreadsheet and Candidate Tracker sheet.

Replace recruiter@example.com and https://example.com/assessment with your own values.

Publish the n8n workflow and copy its production webhook URL.

In form/NuDesk_Employee_Referral_Form.html, replace:

const WEBHOOK_URL = "https://YOUR-N8N-INSTANCE/webhook/candidate-referral";

with your own production webhook URL.

Reliability and security

The workflow includes:

Duplicate candidate detection before AI processing

Retry logic for CV extraction and AI evaluation

A Processing Error path so failed applications are not lost

Structured AI output validation

Timestamp-based row updates to avoid updating the wrong candidate

Sanitized repository files with no API keys, OAuth tokens, live webhook URL, or private assessment URL

Future improvements

For a production implementation, the next steps would include application IDs instead of timestamp matching, centralized error logging/monitoring, authenticated intake, ATS/CRM integration, and source-agnostic candidate intake.

NuDesk Recruiting Demo — AI-powered recruiting operations workflow