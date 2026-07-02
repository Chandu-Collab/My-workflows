# 🤖 AI Website Chatbot with Memory

An AI-powered website chatbot built with **n8n**, **Google Sheets**, and an **OpenAI-compatible AI model**. This workflow enables contextual conversations by remembering previous messages, storing chat history, and generating intelligent responses through a webhook API.

---

## ✨ Features

- 🤖 AI-powered conversational chatbot
- 🧠 Persistent conversation memory
- 📊 Google Sheets as conversation storage
- 🌐 Webhook API for website integration
- 💬 Context-aware AI responses
- 🔄 Multi-turn conversations
- ⚡ Easy to customize
- 🛠 Beginner-friendly workflow
- 🔌 Compatible with OpenAI-compatible AI providers

---

# 📌 How It Works

```
User Message
      │
      ▼
Webhook
      │
      ▼
Extract Request Data
      │
      ▼
Load Conversation History
      │
      ▼
Format Conversation History
      │
      ▼
AI Agent
      │
      ▼
Merge Response
      │
      ▼
Save User Message
      │
      ▼
Save Assistant Response
      │
      ▼
Respond to Webhook
```

---

# 🚀 Use Cases

- Business Websites
- Customer Support Chatbots
- SaaS Applications
- Portfolio Websites
- FAQ Assistants
- Internal Knowledge Assistants
- AI Website Assistants

---

# 🛠 Requirements

Before using this workflow, configure the following:

- n8n
- Google Sheets Credentials
- OpenAI-compatible AI Model Credentials
- Google Sheet for storing conversations

---

# 📊 Google Sheet Structure

Create a sheet named **Messages** with the following columns:

| ConversationId | role | messages | timestamp |
|----------------|------|----------|-----------|
| abc123 | user | Hello | 2026-07-01T07:30:00Z |
| abc123 | assistant | Hello! How can I help you today? | 2026-07-01T07:30:02Z |

> **Note:** Keep the column names exactly as shown.

---

# 📥 Webhook Request

Send a POST request:

```json
{
  "conversationId": "abc123",
  "message": "Hello"
}
```

---

# 📤 Webhook Response

```json
{
  "ConversationId": "abc123",
  "role": "assistant",
  "timestamp": "2026-07-01T07:30:02Z",
  "messages": "Hello! How can I help you today?"
}
```

---

# 🧠 Conversation Memory

The chatbot remembers previous messages by storing every user and assistant interaction in Google Sheets.

For every new request:

1. Conversation history is loaded.
2. Previous messages are formatted.
3. The AI receives the conversation history along with the latest message.
4. The response is generated.
5. Both the user message and AI response are saved.

This enables natural, context-aware conversations.

---

# ⚙ Workflow Nodes

| Step | Node |
|------|------|
| 1 | Receive Chat Request |
| 2 | Extract Request Data |
| 3 | Load Conversation Memory |
| 4 | Format Conversation History |
| 5 | AI Chat Assistant |
| 6 | Merge AI Response |
| 7 | Save User Message |
| 8 | Prepare Final Response |
| 9 | Save Assistant Reply |
|10 | Return Chat Response |

---

# 🔧 Setup Guide

## 1. Configure AI Credentials

Connect your preferred OpenAI-compatible AI provider.

Examples:

- NVIDIA AI
- OpenAI
- OpenRouter
- Azure OpenAI

---

## 2. Configure Google Sheets

Connect your Google account and select the correct spreadsheet in every Google Sheets node.

---

## 3. Configure the Webhook

Use the **Test URL** while building.

After testing successfully, switch to the **Production URL** for your application or website.

---

## 4. Test the Workflow

Example request:

```json
{
  "conversationId": "abc123",
  "message": "My name is John."
}
```

Follow-up request:

```json
{
  "conversationId": "abc123",
  "message": "What is my name?"
}
```

The AI should remember the previous message and answer correctly.

---

# 📦 Customization

You can easily customize:

- AI Model
- System Prompt
- Conversation Style
- Response Tone
- Storage Backend

---

# 📈 Future Enhancements

Possible upgrades include:

- PostgreSQL or Supabase Memory
- PDF Knowledge Base (RAG)
- Website Crawling
- Human Handoff
- Voice Support
- Multi-language Support
- Conversation Analytics
- CRM Integration

---

# 📄 License

This workflow is provided as a template and may be modified for personal or commercial use.

---

# 🙌 Contributing

Contributions, improvements, and suggestions are welcome.

If you find this workflow useful, consider giving the repository a ⭐.