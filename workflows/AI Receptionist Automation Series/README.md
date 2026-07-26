# 🤖 AI Receptionist Automation
### Production-Ready AI Customer Support Workflow Built with n8n + AI

![License](https://img.shields.io/badge/license-MIT-blue)
![n8n](https://img.shields.io/badge/Built%20With-n8n-red)
![AI](https://img.shields.io/badge/AI-Powered-green)

---

# 📖 Overview

AI Receptionist is an intelligent customer support workflow that automates customer interactions using AI.

Instead of manually responding to every inquiry, the AI classifies customer intent and automatically performs the required action.

The workflow supports four major business scenarios:

✅ FAQ Assistant

✅ Appointment Booking

✅ Lead Capture

✅ Human Escalation

Everything is automated using n8n.

---

# 🎯 Features

✔ AI Intent Detection

✔ FAQ Automation

✔ Appointment Booking

✔ Google Calendar Integration

✔ Lead Qualification

✔ Google Sheets CRM

✔ Gmail Notifications

✔ Human Escalation

✔ Real-Time Responses

✔ Production Ready

---

# 🏗 Workflow Architecture

```
                   Webhook
                      │
                      ▼
               Edit Fields
                      │
                      ▼
              AI Intent Agent
                      │
                      ▼
                Parse JSON
                      │
                      ▼
                   Switch
        ┌────────┼──────────┬──────────┐
        │        │          │          │
      FAQ   Appointment    Lead     Human
```

---

# 📦 Folder Structure

```
AI-Receptionist/

│
├── workflow.json
├── README.md
├── prompts/
│      system_prompt.txt
│
├── documentation/
│      setup-guide.pdf
│      architecture.png
│
├── assets/
│      thumbnails/
│      screenshots/
│
└── examples/
       sample_requests.json
```

---

# 🧠 AI Intent Classification

The AI classifies every incoming message into one of four intents.

```
faq
appointment
lead
human
```

Example:

Customer:

```
Do you offer Hair Spa?
```

↓

Intent

```
faq
```

---

Customer:

```
Book Hair Spa tomorrow at 5 PM.
```

↓

Intent

```
appointment
```

---

Customer:

```
I'm interested in Hair Spa.
```

↓

Intent

```
lead
```

---

Customer:

```
I want to speak with a human representative.
```

↓

Intent

```
human
```

---

# 🚀 Workflow 1
## FAQ Assistant

Flow

```
Webhook

↓

AI Agent

↓

Business Knowledge

↓

AI Reply

↓

Webhook Response
```

Purpose

Answer customer questions instantly.

Examples

• Services

• Pricing

• Working Hours

• Address

• Business Policies

---

# 📅 Workflow 2
## Appointment Booking

Flow

```
Appointment

↓

Validate

↓

Google Calendar

↓

Availability Check

↓

Create Event

↓

Google Sheets

↓

Email Confirmation

↓

Webhook Response
```

Features

✔ Prevent Double Booking

✔ Google Calendar Sync

✔ Email Confirmation

✔ Appointment Logging

---

# 📈 Workflow 3
## Lead Capture

Flow

```
Lead

↓

Validate Lead

↓

Google Sheets

↓

Email Notification

↓

Webhook Response
```

Captured Data

• Name

• Email

• Phone

• Service

• Timestamp

• Status

---

# 👨‍💼 Workflow 4
## Human Escalation

Flow

```
Human

↓

Prepare Escalation

↓

Google Sheets

↓

Gmail

↓

Webhook Response
```

When AI Escalates

• Customer requests a human

• Complaint

• Refund

• Emergency

• Complex issue

---

# 📄 Google Sheets

## Leads Sheet

Columns

```
Timestamp
Name
Email
Phone
Service
Status
```

---

## Human Escalations

Columns

```
Timestamp

Customer Name

Email

Phone

Reason

Customer Message

Status
```

---

# 📧 Email Notifications

Appointment

```
Appointment Confirmed
```

Lead

```
New Lead Received
```

Human

```
Human Escalation Required
```

---

# 🔌 Webhook Request

```json
{
  "sessionId": "12345",
  "currentTime": "2026-07-26T16:30:00+05:30",
  "customer": {
    "name": "John",
    "email": "john@email.com",
    "phone": "9876543210"
  },
  "appointment": {
    "service": "",
    "date": "",
    "time": ""
  },
  "message": "I want to speak with a human representative."
}
```

---

# 📤 Response

```json
{
  "success": true,
  "reply": "Sure, I'll transfer you to a human representative shortly."
}
```

---

# ⚙ Required Integrations

Google Calendar

Google Sheets

Gmail

OpenAI / NVIDIA AI

n8n

---

# 🛠 Installation

## 1 Clone Repository

```
git clone https://github.com/Chandu-Collab/ai-automation-workflows
```

---

## 2 Import Workflow

Open n8n

↓

Import workflow.json

---

## 3 Configure Credentials

Google Sheets

Google Calendar

Gmail

AI Provider

---

## 4 Update IDs

Spreadsheet ID

Calendar ID

Email Address

---

## 5 Test

Use Postman

```
POST

/webhook/ai-receptionist
```

---

# 📸 Demo

Series Videos

✅ Part 1

Intent Classification

✅ Part 2

Appointment Booking

✅ Part 3

Lead Capture

✅ Part 4

Human Escalation

---

# 🛣 Roadmap

- [x] FAQ Automation

- [x] Appointment Booking

- [x] Lead Capture

- [x] Human Escalation

- [ ] WhatsApp Integration

- [ ] CRM Integration

- [ ] Slack Notifications

- [ ] Analytics Dashboard

- [ ] Voice Receptionist

---

# 🤝 Contributions

Feel free to fork the project, improve it, and submit a Pull Request.

---

# 📜 License

MIT License

---

# ⭐ Support

If this project helped you,

⭐ Star the repository

🍴 Fork the project

📢 Share it with others

---

# 👨‍💻 Author

**Chandra Hasa Reddy**

GitHub:
https://github.com/Chandu-Collab

Instagram:
https://instagram.com/shinka_6c

YouTube:
https://youtube.com/@shinka-6c

---

## ⭐ What's Next?

This README is a solid foundation, but for the Wednesday release I'd go one step further and create a **professional documentation package**, not just a README. That package could include:

- 📘 `README.md` (GitHub landing page)
- 📄 `SETUP_GUIDE.md` (step-by-step installation)
- 🤖 `SYSTEM_PROMPT.md` (AI prompt with explanations)
- 🌐 `API_REFERENCE.md` (webhook request/response and schemas)
- 🏗️ `ARCHITECTURE.md` (workflow diagrams and node explanations)
- ❓ `FAQ.md` (common issues and troubleshooting)
- 📜 `LICENSE`

That structure makes the repository feel like an open-source project rather than just a workflow export, which is more likely to earn stars, forks, and trust from other developers.