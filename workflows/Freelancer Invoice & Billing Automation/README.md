# 💼 Freelancer Invoice & Billing Automation

Generate professional PDF invoices, store them securely, track invoice records, and email clients automatically using **n8n**.

---

## 🚀 Overview

Freelancers and agencies often spend valuable time creating invoices manually, organizing files, and sending them to clients.

This workflow automates the entire process from invoice generation to client delivery.

---

## ✨ Features

- 📄 Generate professional invoices automatically
- 🔢 Create unique invoice numbers
- 💰 Automatically calculate subtotal, tax, and total amount
- 🎨 Generate a clean HTML invoice
- 🖨️ Convert HTML into a professional PDF
- ☁️ Upload invoices to Google Drive
- 📊 Save invoice records in Google Sheets
- 📧 Email invoices directly to clients
- ⚡ Fully automated with a single webhook request

---

## 🛠 Technologies Used

- n8n
- JavaScript
- PDFShift API
- Google Drive API
- Google Sheets API
- Gmail API

---

## 📌 Workflow

```
Webhook
      │
      ▼
Prepare Client Details
      │
      ▼
Generate Invoice Number
      │
      ▼
Calculate Totals
      │
      ▼
Generate HTML Invoice
      │
      ▼
Convert HTML → PDF
      │
      ▼
Upload PDF to Google Drive
      │
      ▼
Merge Invoice + Drive Data
      │
      ▼
Store Invoice Record
      │
      ▼
Send Invoice Email
```

---

## 📥 Input

Example Request

```json
{
  "clientName": "John Doe",
  "email": "john@gmail.com",
  "company": "ABC Solutions",
  "items": [
    {
      "service": "Website Development",
      "quantity": 1,
      "price": 800
    },
    {
      "service": "Hosting",
      "quantity": 1,
      "price": 100
    }
  ],
  "currency": "USD",
  "invoiceDate": "2026-07-03",
  "dueDate": "2026-07-10",
  "tax": 18,
  "notes": "Thank you for your business."
}
```

---

## 📤 Output

✔ Professional PDF Invoice

✔ Google Drive Backup

✔ Google Sheets Record

✔ Client Email with PDF Attachment

---

## 📊 Google Sheets Columns

- Invoice Number
- Client Name
- Company
- Email
- Currency
- Amount
- Tax
- Tax Amount
- Subtotal
- Invoice Date
- Due Date
- Status
- Reminder Count
- PDF Name
- Google Drive File ID
- Drive View Link
- Drive Download Link
- Created At

---

## 📧 Email Includes

- Professional invoice message
- Invoice details
- Due date
- Google Drive invoice link
- PDF attachment

---

## 🔧 Required Credentials

Before running this workflow, configure the following credentials inside n8n:

- Google Drive
- Google Sheets
- Gmail
- PDFShift API Key

---

## 📁 Required Services

Create the following before importing:

- Google Drive Folder
- Google Sheet
- PDFShift Account

---

## ⚙️ Environment

No environment variables required.

Simply configure the required credentials in n8n.

---

## 💡 Use Cases

Perfect for:

- Freelancers
- Agencies
- Consultants
- Developers
- Designers
- Marketing Teams
- Small Businesses

---

## 🔮 Phase 2 (Coming Soon)

- Payment Tracking
- Automatic Reminder Emails
- WhatsApp Notifications
- Payment Gateway Integration
- AI-generated Follow-up Messages
- Invoice Analytics Dashboard
- Recurring Invoice Support

---

## 📸 Workflow Preview

Webhook
↓

Generate Invoice

↓

Create PDF

↓

Upload to Google Drive

↓

Save to Google Sheets

↓

Send Invoice Email

---

## 📄 License

MIT License

---

## ❤️ Built With

Built using **n8n** as part of the **Shinka-6C AI Workflow Collection**.

Real-world automation workflows designed to help businesses save time, reduce manual work, and scale efficiently.