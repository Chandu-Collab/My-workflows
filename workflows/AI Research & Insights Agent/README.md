# 🤖 AI Research & Insights Agent

> Research Any Topic → Analyze Multiple Sources → Deliver a Professional AI Report

The **AI Research & Insights Agent** is an intelligent n8n workflow that automatically researches any topic from the web, analyzes multiple trusted sources using AI, and delivers a structured research report directly to the user's inbox.

Built using **free search tools**, **Jina AI Reader**, **LLMs**, and **n8n**.

---

# ✨ Features

- 🔍 Search any topic using DuckDuckGo
- 🌐 Collect multiple trusted web sources
- 📖 Extract article content using Jina AI Reader
- ✂️ Optimize content for AI context limits
- 🧠 Analyze information using AI
- 📄 Generate Executive Summary
- 💡 Extract Key Insights
- 📊 Identify Important Statistics
- 🚀 Discover Opportunities
- ⚠️ Highlight Risks & Challenges
- 📈 Predict Future Trends
- 🎯 Calculate Confidence Score
- 📧 Automatically send a professional HTML report via email

---

# 🏗 Workflow Architecture

Receive Research Request

⬇

Prepare Request

⬇

DuckDuckGo Search

⬇

Parse Search Results

⬇

Loop Through Search Results

⬇

Jina AI Reader

⬇

Optimize Article Content

⬇

Aggregate Research

⬇

AI Research Analyst

⬇

Generate HTML Report

⬇

Send Research Report (Gmail)

---

# 📥 Input

| Field | Type | Description |
|-------|------|-------------|
| topic | String | Research topic |
| email | String | User email address |

Example

```json
{
  "topic":"AI Agents in Healthcare",
  "email":"user@example.com"
}
```

---

# 📤 Output

The user receives a professional HTML email containing:

- Executive Summary
- Key Insights
- Statistics
- Opportunities
- Risks
- Future Trends
- Conclusion
- Sources
- Confidence Score

---

# 🧠 AI Report Structure

The generated report includes:

- Executive Summary
- Key Insights
- Statistics
- Opportunities
- Risks
- Future Trends
- Conclusion
- Research Sources
- Confidence Score

---

# 🛠 Tech Stack

- n8n
- DuckDuckGo Search
- Jina AI Reader
- OpenAI / Gemini
- Gmail
- JavaScript
- HTML Email Templates

---

# ⚙️ Setup Instructions

## 1. Import Workflow

Import the provided JSON workflow into n8n.

---

## 2. Configure Credentials

Configure:

- OpenAI or Gemini Chat Model
- Gmail OAuth Credentials

---

## 3. Update Webhook URL

Replace the webhook URL with your deployed endpoint.

---

## 4. Execute

Send a POST request:

```json
{
  "topic":"Artificial Intelligence",
  "email":"user@example.com"
}
```

---

# 📧 Email Example

Subject

```
📚 Your AI Research Report is Ready | Artificial Intelligence
```

The report is delivered as a professionally formatted HTML email.

---

# 💼 Use Cases

- Market Research
- Competitor Analysis
- Startup Research
- Healthcare Research
- Technology Research
- Academic Research
- Product Research
- Industry Reports
- Business Intelligence
- Investment Research

---

# 🚀 Future Improvements (Phase-2)

- PDF Report Generation
- Charts & Visualizations
- Citation Quality Scoring
- Scheduled Research Reports
- Multi-language Reports
- Research History Dashboard
- Knowledge Base Integration
- AI Follow-up Questions
- Research Comparison Reports

---

# 📂 Folder Structure

```
AI-Research-Agent/
│
├── workflow.json
├── README.md
├── documentation.pdf
├── blueprint.pdf
├── screenshots/
└── assets/
```

---

# 📌 Notes

- Uses free DuckDuckGo Search.
- Uses Jina AI Reader for webpage extraction.
- Article content is optimized before AI processing to prevent context limit issues.
- Duplicate sources and duplicate insights are automatically removed.

---

# 👨‍💻 Author

**Shinka-6C**

Building practical AI Agents and n8n Automations.

---

# ⭐ Support

If you found this workflow useful:

⭐ Star the repository

🍴 Fork the project

📢 Share it with the community

Follow for more AI Agents and Automation Workflows.

---

## 📜 License

This project is released under the MIT License.