# 🤖 AI Competitor Intelligence Agent

> Automatically monitor competitor websites, detect business changes, and receive instant email alerts.

---

# 📌 Overview

The AI Competitor Intelligence Agent continuously monitors competitor websites, extracts structured business information using AI, compares it with previously stored snapshots, detects meaningful changes, and instantly sends email notifications whenever updates are found.

This workflow is ideal for startups, agencies, SaaS companies, product managers, and marketing teams who need real-time competitor intelligence.

---

# ✨ Features

✅ Monitor multiple competitor websites

✅ Scrape website content automatically

✅ AI extracts structured business information

✅ Store snapshots in Google Sheets

✅ Compare current data with previous snapshots

✅ Detect new products, services, announcements, and research updates

✅ Ignore unchanged competitors

✅ Send instant email alerts

✅ Maintain historical competitor snapshots

---

# 🏗 Workflow Architecture

```
Google Sheets
      │
      ▼
Load Competitor URLs
      │
      ▼
HTTP Request
      │
      ▼
Website Scraper
      │
      ▼
OpenAI Extraction Agent
      │
      ▼
Structured JSON Snapshot
      │
      ▼
Load Previous Snapshot
      │
      ▼
New Company?
 ┌───────────────┐
 │               │
Yes             No
 │               │
 ▼               ▼
Save Snapshot   Compare Previous vs Current
                     │
                     ▼
             OpenAI Change Detection
                     │
                     ▼
             Changes Found?
             │           │
            No          Yes
             │           │
             ▼           ▼
           Finish    Send Email Alert
                        │
                        ▼
                 Update Snapshot
```

---

# 🧠 AI Extraction

The first AI Agent extracts structured business information.

It identifies:

- Company Name
- Products
- Services
- Pricing
- Features
- Announcements
- News
- Research
- Careers
- Calls-to-Action

Example Output

```json
{
  "company":"OpenAI",
  "products":[
    "ChatGPT",
    "GPT-5.6"
  ],
  "services":[
    "API Platform"
  ],
  "features":[
    "GPT Live"
  ]
}
```

---

# 🔍 AI Change Detection

The second AI Agent compares

Previous Snapshot

↓

Current Snapshot

and determines

- Added products
- Removed products
- Updated services
- New announcements
- Research updates
- Website changes

Example

```json
{
  "changed": true,
  "impact": "Medium",
  "summary": "Two new products detected.",
  "changes":[
      "Added GPT-6",
      "New pricing page"
  ]
}
```

---

# 📧 Email Notification

Whenever meaningful changes are detected, the workflow automatically sends an email.

Example

```
Subject

🚨 Competitor Update Detected

Body

Company:
OpenAI

Changes Detected

• New Product Added
• New Announcement
• Updated Features

Impact

Medium

Summary

OpenAI launched GPT-6 and updated pricing.
```

---

# 📊 Google Sheets Structure

## Companies Sheet

| Company | Website |
|----------|----------|
| OpenAI | https://openai.com |
| Anthropic | https://anthropic.com |
| Perplexity | https://perplexity.ai |

---

## Snapshots Sheet

| Company | Snapshot | Last Checked |
|----------|-----------|---------------|

The snapshot column stores the complete JSON output from the AI Extraction Agent.

---

# 🔧 Required Integrations

- OpenAI
- Google Sheets
- Gmail
- HTTP Request
- JavaScript Code Nodes

---

# 📂 Required n8n Nodes

- Manual Trigger
- Google Sheets
- HTTP Request
- Code
- AI Agent
- Merge
- IF
- Gmail

---

# ⚙️ Setup Guide

## Step 1

Import the workflow into n8n.

---

## Step 2

Create a Google Sheet containing:

Companies

Snapshots

---

## Step 3

Add competitor websites.

Example

- OpenAI
- Anthropic
- Perplexity

---

## Step 4

Configure credentials.

- Google Sheets
- Gmail
- OpenAI

---

## Step 5

Run the workflow.

The first execution creates snapshots.

Future executions compare new data against historical snapshots.

---

# 📈 Workflow Logic

```
Load Companies

↓

Fetch Website

↓

Extract Business Data

↓

Load Previous Snapshot

↓

Compare

↓

Changes?

├── No → End

└── Yes

      ↓

Email Alert

↓

Update Snapshot
```

---

# 🎯 Use Cases

- Competitor Monitoring
- Product Intelligence
- Startup Research
- Market Research
- SaaS Tracking
- AI Industry Monitoring
- Product Launch Detection
- Marketing Intelligence

---

# 📸 Demo

Workflow Overview

- Monitor websites
- AI extraction
- Snapshot storage
- AI comparison
- Email notification

---

# 🚀 Future Improvements

- Slack notifications
- Discord alerts
- Microsoft Teams integration
- Weekly competitor reports
- AI-generated competitor summaries
- Trend analysis dashboard
- Multi-language website support
- Change severity scoring
- PDF report generation

---

# 🛠 Tech Stack

- n8n
- OpenAI
- Google Sheets
- Gmail
- JavaScript
- HTTP Request

---

# 👨‍💻 Developed By

**Shinka-6c**

Building practical AI automation workflows for businesses.

⭐ Follow for more AI Agents and Automation Systems.