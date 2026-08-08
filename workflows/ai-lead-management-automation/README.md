🤖 AI Lead Management & Sales Automation

An end-to-end AI-powered lead management and sales automation workflowbuilt with n8n, AI agents, Google Sheets, Gmail, JavaScript, andWebhooks.

Capture → Qualify → Prioritize → Automate

🚀 Overview

This project demonstrates how a customer enquiry moves through acomplete automated sales workflow:

Lead Capture — receives and stores the enquiry.

AI Lead Qualification — understands the customer’s request.

AI Sales Intelligence — scores and prioritizes the lead.

CRM & Follow-up Automation — prepares CRM actions, schedulesfollow-up, and notifies the sales team.

Customer Communication — sends a personalized response.

Webhook Response — returns the final workflow result.

The core design principle is:

AI understands and recommends. Deterministic workflow logicexecutes.

🏗️ Architecture

Postman / Webhook
       ↓
Lead Capture
       ↓
AI Qualification Agent
       ↓
AI Sales Intelligence Agent
       ↓
CRM Automation (JavaScript)
       ↓
 ┌───────────────┬───────────────┐
 ↓               ↓
Responses Sheet  CRM Sheet
 └───────────────┴───────────────┘
       ↓
      Merge
       ↓
Notification Required?
       ├── TRUE  → Internal Sales Email
       └── FALSE → Skip Notification
                    ↓
              Customer Email AI
                    ↓
                  Gmail
                    ↓
             Respond to Webhook

📥 Part 1 — AI Lead Capture

The first stage receives a customer enquiry through a webhook.

Example input

{
  "name": "Chandu",
  "email": "example@email.com",
  "message": "Hello, I need help with a project."
}

Responsibilities

Receive the lead through a webhook.

Preserve customer information.

Generate an initial professional response.

Store the lead.

Send an acknowledgement email.

Flow:

Webhook → Lead Data → AI Response → Storage → Customer Email

🧠 Part 2 — AI Lead Qualification

The qualification agent converts an unstructured customer message intostructured lead intelligence.

Fields generated

Lead Summary

Intent

Category

Pain Point

Urgency

Sentiment

Confidence

Qualification Status

Next Action

Example

{
  "lead_summary": "The customer is seeking personalized career guidance.",
  "intent": "Career Consultation",
  "category": "Consultation",
  "pain_point": "Needs career guidance",
  "urgency": "Medium",
  "sentiment": "Neutral",
  "confidence": 90,
  "qualification_status": "Qualified",
  "next_action": "Schedule Consultation"
}

The qualification layer focuses on understanding the lead, whilesales intelligence focuses on business value.

📈 Part 3 — AI Sales Intelligence

A second AI agent evaluates the qualified lead and produces actionablesales intelligence.

Fields generated

Lead Score

Lead Temperature

Sales Priority

Conversion Probability

Response Time

Opportunity Level

Sales Recommendation

Follow-up Required

Example

{
  "lead_score": 97,
  "lead_temperature": "Hot",
  "sales_priority": "High",
  "conversion_probability": "High",
  "response_time": "Immediately",
  "opportunity_level": "High",
  "sales_recommendation": "Assign Sales Representative",
  "follow_up_required": true
}

Conceptually:

Qualification
      +
Intent
      +
Confidence
      +
Urgency
      +
Sentiment
      ↓
Lead Score
      ↓
Sales Priority
      ↓
Recommended Action

🏢 Part 4 — AI CRM & Follow-up Automation

Part 4 converts the sales intelligence into operational actions.

Rather than adding another AI agent, deterministic JavaScript logiccreates the CRM record and controls downstream automation.

CRM fields

Field

Purpose

CRM Status

Current operational state

Assigned To

Sales/marketing ownership

Follow-up Date

Recommended follow-up date

Last Action

Latest CRM action

Internal Notes

Sales context

Notification Required

Controls notification routing

CRM Updated At

CRM update timestamp

Example

{
  "crm_status": "Pending Contact",
  "assigned_to": "Sales Team",
  "follow_up_date": "2026-08-06",
  "last_action": "CRM Record Created",
  "notification_required": true,
  "status": "CRM Updated"
}

📊 Data Storage

The workflow intentionally separates lead intelligence from CRMoperations.

Responses Sheet

Stores:

Customer information

Lead qualification

Sales intelligence

Typical fields include:

response_id
lead_id
name
email
message
Lead Summary
Intent
Category
Pain Point
Urgency
Sentiment
Confidence
Qualification Status
Next Action
Lead Score
Lead Temperature
Sales Priority
Conversion Probability
Response Time
Opportunity Level
Sales Recommendation
Follow up Required

CRM Sheet

Stores:

CRM Status
Assigned To
Follow-up Date
Last Action
Internal Notes
Notification Required
CRM Updated At

This keeps operational CRM information separate from the mainlead-response dataset.

🔀 Conditional Notification

After the Responses and CRM datasets are merged, an IF node checks:

Notification Required?

TRUE branch

CRM Updated
    ↓
Internal Sales Notification
    ↓
Customer Email

FALSE branch

CRM Updated
    ↓
Skip Internal Notification
    ↓
Customer Email

The customer can still receive a response regardless of whether theinternal notification is required.

🚨 Internal Sales Notification

The internal email is designed for the sales team.

It can contain:

Customer name and email

Intent

Category

Pain point

Lead score

Lead temperature

Sales priority

Conversion probability

Opportunity level

CRM status

Assigned team

Follow-up date

Sales recommendation

Internal notes

Example:

🚨 New Lead Requires Attention

Customer: Chandu
Intent: Project Request
Lead Score: 97
Priority: High

CRM Status: Pending Contact
Assigned To: Sales Team
Follow-up Date: Today

Recommendation:
Assign Sales Representative

📧 Customer Communication

Customer communication is intentionally separated from internal CRMinformation.

The customer receives only relevant information:

Personalized greeting

Confirmation of the enquiry

Understanding of their request

Appropriate next step

Internal fields are not exposed to the customer, including:

Lead Score

Sales Priority

Conversion Probability

CRM Status

Assigned To

Internal Notes

Notification Required

This separation keeps customer communication professional and protectsinternal sales logic.

🔄 Complete Lead Lifecycle

CAPTURE
Customer submits enquiry
        ↓
QUALIFY
AI understands the request
        ↓
PRIORITIZE
AI evaluates sales potential
        ↓
STORE
Lead + intelligence saved
        ↓
AUTOMATE
CRM record prepared
        ↓
DECIDE
Notification required?
    ↙             ↘
  YES              NO
   ↓                ↓
Sales Alert       Skip
    ↘             ↙
      Customer Email
             ↓
      Webhook Response

🧩 Technology Stack

Technology

Purpose

n8n

Workflow orchestration

AI Agents

Qualification, sales intelligence, communication

JavaScript

Deterministic CRM/business logic

Postman

Webhook/API testing

Google Sheets

Lead and CRM storage

Gmail

Customer and internal emails

Webhooks

Workflow entry and response

IF Node

Conditional routing

Merge Node

Combines response and CRM data

🧠 AI vs Workflow Logic

A major design principle is separating probabilistic AI tasks fromdeterministic automation.

AI handles

Natural-language understanding
Intent detection
Lead qualification
Sales intelligence
Personalized customer communication

Workflow logic handles

Data storage
CRM updates
Follow-up scheduling
Conditional routing
Internal notifications
Webhook completion

This avoids using AI where predictable business rules are sufficient.

🧪 Testing

High-priority test

We want to build a custom AI automation platform.

Expected flow:

High Sales Priority
       ↓
CRM Updated
       ↓
Notification Required = true
       ↓
Sales Team Notification

Low-priority test

Hi, I'm just browsing your services and gathering some general information. I don't have any immediate requirements.

Expected flow:

Low Sales Priority
       ↓
CRM Updated
       ↓
Notification Required = false
       ↓
Internal Notification Skipped

Because AI classification can vary by model and prompt, test casesshould be validated against the project’s configured business rules.

⚙️ Setup

Prerequisites

Running n8n instance

Configured AI model/provider

Google Sheets credentials

Gmail credentials

Postman or another HTTP client

Basic setup

Import the n8n workflow.

Configure AI credentials.

Configure Google Sheets credentials.

Configure Gmail credentials.

Connect the Responses and CRM sheets.

Configure the webhook.

Verify the AI prompts.

Send a test request through Postman.

Verify the Google Sheets records and emails.

Activate the workflow.

Never commit API keys, OAuth tokens, passwords, or privatecredentials.

📁 Suggested Repository Structure

ai-lead-management-automation/
│
├── README.md
│
├── workflows/
│   ├── part-1-lead-capture.json
│   ├── part-2-lead-qualification.json
│   ├── part-3-sales-intelligence.json
│   └── part-4-crm-automation.json
│
├── docs/
│   ├── setup.md
│   ├── architecture.md
│   ├── ai-prompts.md
│   ├── google-sheets-schema.md
│   └── testing.md
│
├── examples/
│   ├── sample-input.json
│   ├── qualification-output.json
│   ├── sales-intelligence-output.json
│   └── crm-output.json
│
├── screenshots/
│   ├── workflow/
│   ├── google-sheets/
│   ├── crm/
│   └── email/
│
└── .gitignore

🎥 Four-Part Series

This project was built and demonstrated as a four-part series:

Part 1 — AI Lead Capture

Receive, store, and respond to incoming leads.

Part 2 — AI Lead Qualification

Turn customer messages into structured lead intelligence.

Part 3 — AI Sales Intelligence

Score and prioritize leads for sales action.

Part 4 — AI CRM & Follow-up Automation

Turn sales intelligence into CRM updates, internal notifications,follow-up actions, and customer communication.

🔮 Future Improvements

Potential extensions:

Replace Google Sheets with PostgreSQL or Supabase.

Integrate HubSpot or Salesforce.

Add Slack/Discord notifications.

Build a sales dashboard.

Add persistent follow-up reminders.

Add retry and error handling.

Add human approval for high-impact actions.

Add authentication and role-based access.

Add conversion analytics.

Introduce queue-based processing for larger workloads.

These are future improvements and are not claimed as implementedfeatures of the current workflow.

🎯 Project Philosophy

The goal is not simply to demonstrate multiple AI agents.

It demonstrates how AI and deterministic automation can work together tocomplete a real business process:

AI understands
      ↓
AI evaluates
      ↓
Workflow executes
      ↓
CRM updates
      ↓
Sales team is notified
      ↓
Customer receives a response

Capture → Qualify → Prioritize → Automate

📌 Summary

This project demonstrates an end-to-end AI-powered lead management andsales automation pipeline built with n8n.

It combines:

Structured AI outputs

Multiple specialized AI agents

Deterministic JavaScript business logic

Google Sheets data persistence

CRM automation

Conditional notifications

Customer communication

Webhook-based workflow execution

The result is a practical automation pipeline that connects AIreasoning with real business operations.