🤖 AI Quote Generator

An end-to-end business quotation automation built with n8n.

The AI Quote Generator automates the complete quotation lifecycle — from receiving a quote request to generating a professional PDF, delivering it to the customer, tracking interactions, handling acceptance or rejection, and automatically sending follow-up emails.

Built as part of the Shinka.ai Automation Series.

✨ Features
📄 Phase 1 — Quote Generation
Receive quotation requests through a webhook
Validate incoming quote data
Generate a unique Quote ID
Process customer and business information
Calculate quotation pricing
Generate structured quotation content
📑 Phase 2 — PDF Generation & Delivery
Generate a professional quotation PDF
Upload the PDF to Google Drive
Generate PDF view and download links
Store quotation information in Google Sheets
Automatically send the quotation to the customer via Gmail

The quotation email includes:

Quote ID
Total quotation amount
Validity period
View Quote button
Download PDF button
👀 Phase 3 — Quote Tracking & Customer Actions

The system tracks customer interactions with the quotation.

View Tracking

When the customer clicks View Quote:

SENT → VIEWED

The workflow:

Receives the quote_id
Finds the quotation in Google Sheets
Validates the quote
Updates the status to VIEWED
Stores the viewed_at timestamp
Redirects the customer to the quotation PDF
✅ Quote Acceptance

When the customer clicks Accept Quote:

SENT / VIEWED → ACCEPTED

The workflow:

Validates the Quote ID
Checks whether the quote is still valid
Updates the quote status
Records the customer action
Stores the action timestamp
Stops future follow-ups
❌ Quote Rejection

When the customer clicks Reject Quote:

SENT / VIEWED → REJECTED

The workflow:

Validates the Quote ID
Checks the quote status
Updates the quotation to REJECTED
Stores the rejection timestamp
Records the customer action
Stops future follow-ups
⏳ Quote Expiry

Each quotation has a validity period.

If the quotation passes its valid_until date, it can be marked as:

EXPIRED

Expired quotations are excluded from follow-up processing.

🔁 Phase 4 — Automated Follow-ups

The workflow automatically monitors active quotations and sends follow-up emails.

A follow-up is sent only when the quotation:

Has a status of SENT or VIEWED
Is not ACCEPTED
Is not REJECTED
Is not EXPIRED
Has not reached the maximum follow-up limit
Has reached its next follow-up time

Current configuration:

Follow-up interval: 3 days
Maximum follow-ups: 5

After every follow-up, the workflow updates:

follow_up_count
last_follow_up_at
next_follow_up_at
🏗️ Complete Workflow
QUOTE REQUEST
      │
      ▼
VALIDATE INPUT
      │
      ▼
GENERATE QUOTE ID
      │
      ▼
PROCESS QUOTATION
      │
      ▼
GENERATE PDF
      │
      ▼
UPLOAD PDF TO GOOGLE DRIVE
      │
      ▼
STORE QUOTE IN GOOGLE SHEETS
      │
      ▼
SEND QUOTATION EMAIL
      │
      ▼
┌─────────────────────────────┐
│     CUSTOMER INTERACTION     │
└─────────────────────────────┘
      │
      ├───────────────┐
      │               │
      ▼               ▼
 VIEW QUOTE      CUSTOMER ACTION
      │               │
      ▼               ├───────────────┐
 UPDATE STATUS          │               │
 TO VIEWED              ▼               ▼
      │              ACCEPT          REJECT
      │                 │               │
      │                 ▼               ▼
      │             ACCEPTED        REJECTED
      │                 │               │
      └─────────────────┴───────────────┘
                        │
                        ▼
                FOLLOW-UP SYSTEM
                        │
                        ▼
            CHECK EVERY ACTIVE QUOTE
                        │
              ┌─────────┴─────────┐
              │                   │
              ▼                   ▼
        FOLLOW-UP DUE        NO ACTION
              │
              ▼
         SEND FOLLOW-UP
              │
              ▼
      UPDATE FOLLOW-UP DATA
              │
              ▼
        MAXIMUM 5 FOLLOW-UPS
📊 Quote Status Lifecycle
GENERATED
    │
    ▼
SENT
    │
    ▼
VIEWED
    │
    ├───────────────┐
    │               │
    ▼               ▼
ACCEPTED         REJECTED
    │               │
    └───────┬───────┘
            │
            ▼
     STOP FOLLOW-UPS

A quotation can also become:

EXPIRED

The terminal statuses are:

ACCEPTED
REJECTED
EXPIRED

Once a quote reaches one of these statuses, it is excluded from future follow-ups.

🛠️ Tech Stack
Technology	Purpose
n8n	Workflow automation
Google Sheets	Quote storage and status tracking
Google Drive	PDF storage
Gmail	Quote and follow-up emails
Webhooks	Quote requests and customer actions
JavaScript	Validation and workflow logic
ngrok / Public URL	Exposing self-hosted webhooks
📋 Google Sheets Setup

Create a Google Sheet with the following columns.

Column	Description
quote_id	Unique quotation ID
status	Current quote status
customer_name	Customer name
customer_email	Customer email
total	Total quotation amount
currency	Currency code
pdf_view_url	PDF view URL
pdf_download_url	PDF download URL
created_at	Quote creation timestamp
valid_until	Quote validity timestamp
generated_at	PDF generation timestamp
sent_at	Initial quotation email timestamp
viewed_at	Quote viewed timestamp
accecpted_at	Quote acceptance timestamp
rejected_at	Quote rejection timestamp
expired_at	Quote expiry timestamp
customer_action	Latest customer action
customer_action_at	Customer action timestamp
follow_up_count	Number of follow-ups sent
last_follow_up_at	Last follow-up timestamp
next_follow_up_at	Next scheduled follow-up timestamp

Note: The workflow currently uses accecpted_at as the column name. If you change it to accepted_at, update the related mappings and expressions inside the workflow.

🚀 Getting Started
1. Import the Workflow

Download the workflow JSON file from the `workflows/` directory in the Shinka repository.

Open your n8n instance and import the workflow.

Workflows
   ↓
Import from File
   ↓
Select Workflow JSON

After importing, configure all required credentials and resources.

2. Configure Google Sheets

Create a Google Spreadsheet using the columns listed above.

Inside the Google Sheets nodes:

Connect your Google account
Select your spreadsheet
Select the correct sheet
Verify that all column mappings match your sheet

The workflow uses quote_id to identify and update the correct quotation.

3. Configure Google Drive

Connect your Google Drive account to n8n.

The workflow uploads generated quotation PDFs to Google Drive.

After uploading, configure the workflow to generate:

View URL
https://drive.google.com/file/d/FILE_ID/view
Download URL
https://drive.google.com/uc?id=FILE_ID&export=download

These URLs are stored in Google Sheets and used in the customer email.

4. Configure Gmail

Connect your Gmail account in n8n.

Gmail is used for:

Sending the original quotation
Sending automated follow-up emails

Make sure the Gmail nodes use your configured credentials.

🌐 Webhook Configuration

The workflow uses webhooks for quotation requests and customer interactions.

The exact paths may vary depending on your imported workflow.

Example structure:

Generate Quote
POST /webhook/quote
View Quote
GET /webhook/quote/view?quote_id=QUOTE_ID
Accept Quote
GET /webhook/quote/action?action=accept&quote_id=QUOTE_ID
Reject Quote
GET /webhook/quote/action?action=reject&quote_id=QUOTE_ID

Replace the webhook base URL with your own n8n instance or public domain.

Example:

https://your-domain.com/webhook/quote/action
📧 Customer Email Actions

The quotation email can contain four main actions:

VIEW QUOTE
     ↓
Tracks quotation view
     ↓
Updates status → VIEWED


DOWNLOAD PDF
     ↓
Downloads quotation PDF


ACCEPT QUOTE
     ↓
Updates status → ACCEPTED


REJECT QUOTE
     ↓
Updates status → REJECTED

All actions use the quotation's unique quote_id.

🔁 Follow-up System

The follow-up workflow checks every quotation stored in Google Sheets.

A quotation is eligible for follow-up when:

Status = SENT or VIEWED

AND

Quote is not expired

AND

Status is not ACCEPTED

AND

Status is not REJECTED

AND

Follow-up count < Maximum Follow-ups

AND

Current time >= next_follow_up_at

Current configuration:

const FOLLOW_UP_AFTER_DAYS = 3;
const MAX_FOLLOW_UPS = 5;

You can change these values based on your business requirements.

For example:

const FOLLOW_UP_AFTER_DAYS = 2;
const MAX_FOLLOW_UPS = 3;
📈 Follow-up Lifecycle
QUOTE SENT
     │
     ▼
WAIT 3 DAYS
     │
     ▼
FOLLOW-UP #1
     │
     ▼
UPDATE GOOGLE SHEETS
     │
     ├── follow_up_count + 1
     ├── last_follow_up_at = NOW
     └── next_follow_up_at = NOW + 3 DAYS
     │
     ▼
WAIT UNTIL NEXT FOLLOW-UP
     │
     ▼
FOLLOW-UP #2
     │
     ▼
...
     │
     ▼
MAXIMUM 5 FOLLOW-UPS

Follow-ups automatically stop when:

ACCEPTED
REJECTED
EXPIRED
MAXIMUM FOLLOW-UP LIMIT REACHED
🧪 Example Quote Request

Below is a simplified example request body.

{
  "customer": {
    "name": "ABC Technologies",
    "email": "customer@example.com"
  },
  "currency": "INR",
  "pricing": {
    "total": 59000
  },
  "validity_days": 7
}

Your exact request body may vary depending on your workflow configuration.

📁 Suggested Directory Structure
AI-Quote-Generator/
│
├── README.md
│
├── workflows/
│   ├── ai-quote-generator.json
│   ├── quote-view-tracking.json
│   ├── quote-action-handler.json
│   └── quote-follow-up.json
│
├── examples/
│   └── sample-request.json
│
├── screenshots/
│   ├── workflow-overview.png
│   ├── quote-email.png
│   ├── google-sheets-tracking.png
│   └── follow-up-email.png
│
└── LICENSE
⚙️ Required Credentials

Before running the workflow, configure the following credentials in n8n:

Google Sheets
Google Drive
Gmail

You may also need to configure:

Public webhook URL
PDF generation service or node
AI provider credentials, depending on your workflow configuration
🔐 Security Recommendations

The current workflow is designed as an educational and practical automation project.

Before using a similar setup in production, consider implementing:

Webhook authentication
Signed action URLs
Secure tokens
Token expiration
Rate limiting
Input validation
Quote ownership validation
Error handling and logging

For example, instead of exposing only:

?quote_id=QT-XXXXXX

A production system can use a secure token:

?quote_id=QT-XXXXXX&token=SECURE_RANDOM_TOKEN

This helps prevent unauthorized quote actions.

📸 Screenshots

Add screenshots here to help users understand the workflow.

Recommended screenshots:

1. Complete n8n Workflow
2. Quote Request / Webhook Input
3. Generated Quotation PDF
4. Customer Email
5. View / Accept / Reject Actions
6. Google Sheets Status Tracking
7. Automated Follow-up Email

Example:

![Workflow Overview](screenshots/workflow-overview.png)

![Quotation Email](screenshots/quote-email.png)

![Google Sheets Tracking](screenshots/google-sheets-tracking.png)

![Follow-up Email](screenshots/follow-up-email.png)
✅ Complete Feature Checklist
 Quote generation
 Input validation
 Unique Quote ID generation
 Dynamic pricing
 Professional PDF generation
 Google Drive PDF storage
 PDF view URL
 PDF download URL
 Google Sheets quote storage
 Quotation email delivery
 Quote view tracking
 VIEWED status update
 Quote acceptance
 Quote rejection
 Customer action tracking
 Customer action timestamps
 Quote validity checking
 Quote expiry handling
 Automated follow-up detection
 Configurable follow-up interval
 Maximum follow-up limit
 Follow-up history tracking
 Automatic follow-up stopping
🎯 Complete Automation Summary
INPUT
  ↓
VALIDATION
  ↓
QUOTE GENERATION
  ↓
PDF GENERATION
  ↓
GOOGLE DRIVE
  ↓
GOOGLE SHEETS
  ↓
CUSTOMER EMAIL
  ↓
CUSTOMER INTERACTION
  ↓
VIEWED / ACCEPTED / REJECTED
  ↓
AUTOMATED FOLLOW-UP SYSTEM
  ↓
TRACK EVERY QUOTE UNTIL COMPLETION
🤝 Contributing

Feel free to:

Fork the Shinka repository
Explore the workflow
Customize it for your own business
Improve the automation
Submit issues or suggestions

If you build something using this project, feel free to share your implementation! 🚀

📜 License

This project is released under the license included in the Shinka repository.

Please check the main LICENSE file in the root directory for complete terms and conditions.

🌟 Shinka.ai

This project is part of the Shinka.ai automation initiative.

Shinka.ai focuses on building practical automation systems, AI agents, and workflows that solve real-world problems.

More workflows, documentation, and automation resources will be added to the platform.

🚀 Keep Building. Keep Learning. Keep Growing.