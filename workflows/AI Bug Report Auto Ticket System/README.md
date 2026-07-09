# 🐞 AI Bug Report Auto Ticket System

> Automatically convert bug reports into structured engineering tickets using AI.

![Version](https://img.shields.io/badge/version-1.0.0-red)
![Release](https://img.shields.io/badge/release-Phase--1-success)
![Platform](https://img.shields.io/badge/Built%20With-n8n-orange)
![AI](https://img.shields.io/badge/Powered%20By-AI-blue)

---

## 📖 Overview

The **AI Bug Report Auto Ticket System** is an intelligent workflow built with **n8n** that automates the complete bug reporting process.

Instead of manually reviewing bug reports and creating engineering tickets, this workflow uses AI to analyze the submitted issue, determine its severity and priority, generate a structured ticket, store it in Google Sheets, and notify the reporter automatically.

---

## ✨ Features

- 📥 Receive bug reports through a Webhook
- 🤖 AI-powered bug analysis
- 🏷️ Automatic category detection
- 🚨 AI-based severity classification
- ⚡ Priority assignment
- 📝 Structured engineering ticket generation
- 📊 Store tickets in Google Sheets
- 📧 Send confirmation email automatically
- 🎫 Generate unique Ticket IDs
- 📋 Maintain standardized ticket metadata

---

# 🏗 Workflow Architecture

```
User
 │
 ▼
Webhook
 │
 ▼
Prepare Bug Report
 │
 ▼
AI Bug Analysis
 │
 ▼
Parse AI Response
 │
 ▼
Merge Data
 │
 ▼
Create Master Ticket
 │
 ▼
Google Sheets
 │
 ▼
Confirmation Email
```

---

# 🧠 AI Responsibilities

The AI Agent automatically:

- Understands the reported issue
- Identifies the affected system
- Categorizes the bug
- Determines severity
- Determines priority
- Creates a technical summary
- Estimates business impact
- Suggests possible root causes

---

# 📋 Workflow Steps

### Step 1

Receive bug report through Webhook.

---

### Step 2

Prepare and validate incoming data.

---

### Step 3

Send the report to the AI Agent.

---

### Step 4

Analyze the issue and generate structured output.

---

### Step 5

Parse the AI response into JSON.

---

### Step 6

Merge original user data with AI analysis.

---

### Step 7

Generate the Master Ticket.

Includes:

- Ticket ID
- Status
- Metadata
- Timestamps
- Assignment
- Version

---

### Step 8

Store the ticket in Google Sheets.

---

### Step 9

Send confirmation email to the reporter.

---

# 📥 Input

Example request

```json
{
  "reporter_name": "John Smith",
  "reporter_email": "john@example.com",
  "application": "Shinka-6C Dashboard",
  "environment": "Production",
  "browser": "Chrome",
  "device": "Windows 11",
  "page_url": "https://app.example.com/login",
  "bug_title": "Unable to Login",
  "bug_description": "Users receive HTTP 500 error.",
  "steps_to_reproduce": "Open login page and submit valid credentials.",
  "expected_result": "User should login successfully.",
  "actual_result": "HTTP 500 Internal Server Error."
}
```

---

# 📤 Output

```json
{
  "ticket_id": "BUG-20260707-1292",
  "ticket_type": "Bug",
  "status": "Open",
  "report_status": "Submitted",
  "category": "Backend",
  "severity": "Critical",
  "priority": "P0",
  "technical_summary": "...",
  "business_impact": "...",
  "assigned_to": "Unassigned"
}
```

---

# 🛠 Technologies Used

- n8n
- AI Agent
- JavaScript
- Google Sheets
- Gmail
- Webhooks

---

# 📦 Integrations

- Google Sheets
- Gmail
- AI Model
- Webhook

---

# 📊 Ticket Metadata

Every generated ticket includes:

- Ticket ID
- Ticket Type
- Status
- Report Status
- Created Date
- Updated Date
- Assigned To
- Source
- Version
- Resolution

---

# 💼 Business Use Cases

Perfect for:

- SaaS Platforms
- Software Companies
- QA Teams
- Development Teams
- Internal IT Teams
- Product Teams
- Customer Support Teams

---

# 🚀 Future Improvements

- Jira Integration
- GitHub Issues
- ClickUp Integration
- Linear Integration
- Duplicate Bug Detection
- Screenshot Analysis
- AI Suggested Fixes
- SLA Tracking
- Dashboard & Analytics
- Slack Notifications
- Discord Notifications
- Microsoft Teams Notifications

---

# 📈 Benefits

✅ Reduce manual bug triaging

✅ Standardize engineering tickets

✅ Improve issue prioritization

✅ Faster developer response

✅ Better issue tracking

✅ Automated user communication

---

# 📸 Demo

> Replace with your YouTube demonstration link.

```
YouTube:
https://YOUR_VIDEO_LINK
```

---

# 🌐 Links

Website

```
https://YOUR_WEBSITE
```

Documentation

```
https://YOUR_DOCUMENTATION
```

GitHub

```
https://YOUR_GITHUB
```

---

# 👨‍💻 Developed By

### Shinka-6C

Building real-world AI Automation workflows with n8n.

🌐 Website

Replace with your official website.

---

## ⭐ Support

If you found this workflow helpful:

⭐ Star the repository

👍 Share the project

🚀 Follow Shinka-6C for more AI automation workflows

---

## 📄 License

This project is released for educational and demonstration purposes.

© Shinka-6C