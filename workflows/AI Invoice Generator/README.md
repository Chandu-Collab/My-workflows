Invoice Generator

A complete invoice lifecycle automation built with n8n, Google
Sheets, Google Drive, and Gmail.

The Invoice Generator automates an invoice from creation and delivery
through due-date tracking, payment reminders, and payment confirmation.

🚀 What It Does

The agent is organized into three development phases:

Phase                   Flow                    Purpose

Phase 1             Create → Store →      Generate and deliver a
Email                 professional invoice

Phase 2             Track → Remind →      Monitor due dates and
Record                automate payment
reminders

Together, the phases create one complete invoice lifecycle:

CREATE
  ↓
CALCULATE
  ↓
STORE
  ↓
EMAIL
  ↓
TRACK
  ↓
REMIND
  ↓
PAY
  ↓
CONFIRM
  ↓
PAID
  ↓
STOP FUTURE REMINDERS

✨ Features

Phase 1 --- Create → Store → Email

Receive invoice details through a webhook

Validate invoice data

Prepare and normalize invoice information

Calculate:

Subtotal

Discount

Tax

Grand Total

Amount Due

Generate a professional HTML invoice

Convert the invoice into a PDF

Store the PDF in Google Drive

Record invoice information in Google Sheets

Email the invoice to the customer

Phase 2 --- Track → Remind → Record

Read invoice records from Google Sheets

Check invoice payment status

Calculate days until the due date

Detect:

upcoming

due_soon

due_today

overdue

paid

Automatically decide whether a reminder is required

Send payment reminder emails

Record the last reminder timestamp

Maintain reminder count

Skip reminders when no action is required

Phase 3 --- Pay → Confirm → Stop

Receive payment confirmation through a webhook

Validate payment confirmation data

Find the invoice using its invoice number

Mark the invoice as paid

Set the outstanding amount to 0

Return a payment confirmation response

Reuse Phase 2's existing payment-status logic

Automatically prevent future reminders for paid invoices

Important: Phase 3 is a payment-confirmation workflow. It does not
directly verify a transaction with a bank or payment gateway. A
payment provider integration can be added later.

🏗️ Architecture

The agent is split into three workflows so each responsibility remains
clear and maintainable.

                    INVOICE GENERATOR
                           │
          ┌────────────────┼────────────────┐
          │                │                │
          ▼                ▼                ▼
       PHASE 1          PHASE 2          PHASE 3
       CREATE            TRACK             PAY
          │              REMIND           CONFIRM
        STORE            RECORD            STOP
        EMAIL

Phase 1

Invoice Request
      ↓
Validate Invoice Data
      ↓
Prepare Invoice Data
      ↓
Calculate Invoice
      ↓
Build Invoice Template
      ↓
Generate PDF
      ↓
Store Invoice
      ↓
Prepare Delivery Data
      ↓
Google Sheets Record
      ↓
Email Invoice

Phase 2

Schedule Trigger
      ↓
Get Invoice Records
      ↓
Check Invoice Status
      ↓
Reminder Required?
      ├── YES → Send Payment Reminder
      │              ↓
      │       Update Invoice Record
      │
      └── NO  → Skip

Phase 3

Payment Webhook
      ↓
Validate Payment
      ↓
Find Invoice
      ↓
Mark Invoice as Paid
      ↓
Respond to Payment
      ↓
Phase 2 sees Status = paid
      ↓
action = none
      ↓
No Future Reminder

🧰 Tech Stack

n8n --- Workflow automation

Google Sheets --- Invoice and reminder tracking

Google Drive --- Invoice PDF storage

Gmail --- Invoice delivery and payment reminders

PDF generation service --- HTML invoice to PDF conversion

Postman --- API/webhook testing

📋 Google Sheets Structure

The invoice tracking sheet uses the following columns:

Invoice Number
Customer Name
Customer Email
Invoice Date
Due Date
Currency
Sub Total
Discount
Tax
Grand Total
amount Due
Status
Created At
Last Reminder
Reminder Count

Example

Invoice Number Customer   Due Date        Grand Total     Amount Due Status

INV-2026-001   Chandu     2026-09-10          ₹37,170        ₹37,170 pending

After payment confirmation:

Invoice Number     Amount Due Status

INV-2026-001               ₹0 paid

⚙️ Requirements

Before running the workflows, make sure you have:

An n8n instance

Google account with access to:

Google Sheets

Google Drive

Gmail

A PDF conversion service/API configured for the PDF-generation step

Postman or another HTTP client for testing webhooks

The workflow JSON files from this repository

🔐 Credentials

The workflows require credentials for the services used by the nodes.

Configure the following in n8n:

Google Sheets

Used to:

Create invoice records

Read invoices

Update payment/reminder information

Google Drive

Used to:

Store generated invoice PDFs

Gmail

Used to:

Send invoices

Send payment reminders

PDF Service

Configure the API credentials required by the PDF generation node.

Never commit API keys, OAuth secrets, passwords, or private
credentials to this repository.

📥 Installation

1. Install / open n8n

Use either:

n8n Cloud

A self-hosted n8n instance

A local n8n installation

2. Import the workflows

Import the Phase 1, Phase 2, and Phase 3 workflow JSON files into n8n.

Recommended organization:

workflows/
├── phase-1-invoice-generator.json
├── phase-2-invoice-tracker.json
└── phase-3-payment-confirmation.json

3. Configure credentials

Reconnect/configure the required Google Sheets, Google Drive, Gmail, and
PDF-service credentials in n8n.

4. Configure the Google Sheet

Create the invoice tracking sheet using the column structure shown
above.

5. Update workflow configuration

Check the following before activating the workflows:

Google Sheet ID

Google Drive destination

Gmail sender account

PDF service credentials

Webhook paths

Email addresses

Time/date settings

🧪 Testing

Phase 1 --- Generate an Invoice

Send a POST request to the Phase 1 webhook.

Example:

{
  "business": {
    "name": "Shinka Solutions",
    "email": "billing@shinka.example",
    "phone": "+91 9876543210",
    "address": "Bengaluru, Karnataka, India",
    "taxId": "29ABCDE1234F1Z5"
  },
  "customer": {
    "name": "Chandu",
    "email": "chandouqiande@gmail.com",
    "phone": "+91 9123456789",
    "address": "Bengaluru, Karnataka, India"
  },
  "invoiceNumber": "INV-2026-001",
  "invoiceDate": "2026-08-26",
  "dueDate": "2026-09-10",
  "currency": "INR",
  "items": [
    {
      "description": "Website Development",
      "quantity": 1,
      "unitPrice": 25000
    },
    {
      "description": "Website Maintenance",
      "quantity": 2,
      "unitPrice": 5000
    }
  ],
  "discount": 10,
  "tax": 18,
  "notes": "Thank you for your business."
}

Expected calculation:

Subtotal       = ₹35,000
Discount       = ₹3,500
Taxable Amount = ₹31,500
Tax             = ₹5,670
Grand Total    = ₹37,170
Amount Due     = ₹37,170

The workflow should then:

Generate the invoice PDF

Store it in Google Drive

Record the invoice in Google Sheets

Email the invoice to the customer

📩 Phase 2 --- Test Reminders

The reminder workflow normally runs from its schedule trigger.

For testing, use an invoice with a due date close enough to trigger a
reminder.

Example:

Due Date: 2026-09-01
Current Date: 2026-08-30

Expected result:

invoiceState = due_soon
action       = reminder

The workflow should:

Send Payment Reminder
        ↓
Update Last Reminder
        ↓
Increase Reminder Count

For an invoice that does not require a reminder:

action = none

the reminder branch should be skipped.

💳 Phase 3 --- Confirm Payment

Send a POST request to the Phase 3 payment webhook.

Example:

{
  "invoiceNumber": "INV-2026-001",
  "paymentStatus": "paid"
}

Expected response:

{
  "success": true,
  "message": "Invoice marked as paid",
  "invoiceNumber": "INV-2026-001"
}

The Google Sheet should change from:

Status: pending
amount Due: ₹37,170

to:

Status: paid
amount Due: ₹0

🔗 Phase 2 + Phase 3 Integration Test

After marking an invoice as paid, run the Phase 2 tracking workflow
again.

Because the invoice now has:

Status = paid

the tracking logic should produce:

invoiceState = paid
action       = none

The reminder condition should therefore evaluate to:

FALSE

Result:

No payment reminder is sent.

This verifies that payment confirmation successfully closes the reminder
lifecycle.

🛡️ Payment Validation

Phase 3 accepts only a confirmed paid status.

For example, this is valid:

{
  "invoiceNumber": "INV-2026-001",
  "paymentStatus": "paid"
}

This should fail validation:

{
  "invoiceNumber": "INV-2026-001",
  "paymentStatus": "pending"
}

An invoice number is also required.

📊 Invoice Status Lifecycle

pending
   │
   ├── Upcoming
   │
   ├── Due Soon
   │
   ├── Due Today
   │
   └── Overdue
          │
          │ payment confirmed
          ▼
        paid
          │
          ▼
   No Future Reminders

🔄 Complete Example

A typical invoice moves through the system like this:

1. Customer invoice details received
                ↓
2. Invoice calculated
                ↓
3. PDF generated
                ↓
4. PDF stored in Google Drive
                ↓
5. Invoice recorded in Google Sheets
                ↓
6. Invoice emailed to customer
                ↓
7. Due date monitored
                ↓
8. Payment reminder sent when required
                ↓
9. Payment confirmed
                ↓
10. Invoice marked as paid
                ↓
11. Amount Due becomes 0
                ↓
12. Future reminders automatically skipped

📁 Suggested Repository Structure

invoice-generator/
│
├── workflows/
│   ├── phase-1-invoice-generator.json
│   ├── phase-2-invoice-tracker.json
│   └── phase-3-payment-confirmation.json
│
├── docs/
│   └── setup.md
│
├── examples/
│   ├── invoice-request.json
│   └── payment-confirmation.json
│
├── screenshots/
│
├── README.md
└── LICENSE

Adjust the filenames to match the actual files in the repository.

⚠️ Important Notes

Payment verification

Phase 3 confirms a payment event supplied to the webhook. It does
not independently verify that money was received.

For production use, connect the webhook to a trusted payment provider
and verify its signed/event payload before marking an invoice as paid.

Webhook security

For production deployments, protect webhook endpoints using appropriate
authentication/signature verification rather than exposing an
unrestricted payment endpoint.

Google Sheets

The column names used by the workflows must match the configured sheet
fields.

Phase 2 scheduling

Phase 2 is designed around a scheduled workflow that periodically checks
invoice records. A webhook response is therefore not part of the
scheduled reminder execution itself.

🚀 Future Enhancements

The current version intentionally focuses on the core invoice lifecycle.

Possible future enhancements:

Payment gateway integration

Payment links

Recurring invoices

Customer management

Revenue analytics

Dashboard

Multi-business support

WhatsApp notifications

Multi-currency improvements

GST/e-invoicing integrations

These are intentionally outside the current three-phase implementation.

🎯 Version Summary

Phase 1

Create → Store → Email

Generate professional invoices, store them, record them, and deliver
them automatically.

Phase 2

Track → Remind → Record

Monitor invoice due dates and automate payment reminders.

Phase 3

Pay → Confirm → Stop

Confirm payment, mark invoices as paid, clear the outstanding amount,
and automatically stop future reminders.

⚡ One Complete Invoice Lifecycle

Create → Calculate → Store → Email → Track → Remind → Pay → Confirm →
Paid

Built with n8n + Google Sheets + Google Drive + Gmail.

📄 License

Add your project's chosen license here.

For example:

Copyright © 2026 Shinka / Madduri Chandra Hasa Reddy

See the repository's LICENSE file for the complete license terms.