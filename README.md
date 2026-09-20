# 🤖 AI Career Recommendation System

> **An AI-powered career guidance automation that transforms student profiles into personalized career recommendations, skill-gap insights, and actionable next steps.**

Built with **n8n**, **Google Gemini**, **Google Sheets**, and **Gmail**, this project demonstrates how AI and workflow automation can be combined to create a practical end-to-end career recommendation system.

---

## 📌 Overview

The **AI Career Recommendation System** collects a student's academic background, skills, interests, preferred industry, and career goals through an n8n form.

The submitted information is then processed by **Google Gemini**, which analyzes the profile and generates:

- 🎯 Personalized career recommendations
- 🧩 Relevant skill gaps
- 🚀 Actionable next steps

The generated results are automatically:

1. Stored in **Google Sheets** for record keeping and analysis.
2. Sent to the student through **Gmail**.

This creates a complete automated pipeline from **user input → AI analysis → structured data → personalized email**.

---

## ✨ Key Features

- 📝 **Automated profile collection** using an n8n form
- 🤖 **AI-powered career analysis** using Google Gemini
- 🎯 Personalized career recommendations
- 🧩 Skill-gap identification
- 🚀 Actionable career development steps
- 📊 Automatic storage in Google Sheets
- 📧 Automatic email delivery through Gmail
- 🔄 Fully automated n8n workflow
- 🔐 Credentials removed from the public workflow file
- 📦 Easy to import and customize

---

## 🔄 Workflow Architecture

```text
┌───────────────────────┐
│   Student Form        │
│                       │
│ • Name                │
│ • Email               │
│ • Education           │
│ • Skills              │
│ • Interests           │
│ • Industry             │
│ • Career Goal         │
└───────────┬───────────┘
            │
            ▼
┌───────────────────────┐
│    Edit Fields        │
│                       │
│ Normalize & structure  │
│ submitted information  │
└───────────┬───────────┘
            │
            ▼
┌───────────────────────┐
│    Google Gemini      │
│                       │
│ Analyze student       │
│ profile using AI      │
└───────────┬───────────┘
            │
            ▼
┌───────────────────────┐
│ JavaScript Parser     │
│                       │
│ Convert AI response   │
│ into structured JSON  │
└───────────┬───────────┘
            │
            ▼
     ┌──────┴──────┐
     │             │
     ▼             ▼
┌───────────┐  ┌───────────┐
│  Google   │  │   Gmail   │
│  Sheets   │  │           │
│           │  │ Personalized│
│ Store     │  │ email      │
│ results   │  │ delivery   │
└───────────┘  └───────────┘
```

---

## 🛠️ Technologies Used

| Technology | Purpose |
|---|---|
| **n8n** | Workflow automation and orchestration |
| **Google Gemini** | AI-powered career analysis |
| **JavaScript** | Parsing and structuring Gemini's response |
| **Google Sheets** | Storing recommendations and user data |
| **Gmail** | Delivering personalized recommendations |
| **JSON** | Workflow configuration and structured AI output |

---

# 🚀 Getting Started

## 1. Prerequisites

Before importing the workflow, make sure you have:

- [n8n](https://n8n.io/) installed or an n8n Cloud account
- A Google account
- Access to Google Gemini through n8n
- A Google Sheet
- Gmail access for sending emails

---

## 2. Import the Workflow

1. Open your n8n dashboard.
2. Create a new workflow.
3. Select **Import from File**.
4. Choose:

```text
AI_CAREER_REC_SYSTEM_GITHUB_CLEAN.json
```

5. Open the imported workflow.
6. Configure the required credentials.

---

# 🔑 Credential Configuration

The public workflow intentionally does **not** contain authentication credentials.

You will need to configure the following integrations inside n8n:

### Google Gemini

Connect your Gemini credential to the **Message a model** node.

The workflow uses:

```text
models/gemini-2.5-flash-lite
```

### Google Sheets

Connect your Google account to the **Append row in sheet** node.

Replace the placeholder spreadsheet configuration with your own Google Sheet.

### Gmail

Connect your Gmail account to the **Send a message** node.

The workflow uses the email address submitted through the form as the recipient.

---

# 📊 Google Sheets Setup

Create a Google Sheet with columns corresponding to the information stored by the workflow.

Recommended columns:

```text
Date
Name
Skills
Interests
Skill Gaps
Next Steps
Education Level
Career Recommendations
```

The workflow automatically appends the generated recommendation data to the sheet.

---

# 📝 Form Inputs

The system collects the following information:

| Field | Description |
|---|---|
| **Full Name** | Student's name |
| **Email** | Email address for receiving recommendations |
| **Education Level** | School, Undergraduate, or Postgraduate |
| **Core Skills** | Current technical or professional skills |
| **Interests** | Areas the student enjoys or wants to explore |
| **Preferred Industry** | Industry the student is interested in |
| **Career Goal** | Student's intended career direction |

---

# 🧠 AI Recommendation Output

The Gemini prompt instructs the model to return structured JSON containing three components:

```json
{
  "career_recommendations": [
    "Career option 1",
    "Career option 2"
  ],
  "skill_gaps": [
    "Skill to improve 1",
    "Skill to improve 2"
  ],
  "next_steps": [
    "Action 1",
    "Action 2"
  ]
}
```

This structured response allows n8n to process the AI output automatically instead of treating the recommendation as unstructured text.

---

# ⚙️ Workflow Components

## 1. On Form Submission

The workflow starts when a student submits the career questionnaire.

The form collects the student's:

- Personal information
- Education level
- Skills
- Interests
- Industry preference
- Career goal

---

## 2. Edit Fields

The submitted form data is normalized into consistent field names:

```text
name
email
education_level
skills
interests
preferred_industry
career_goal
submission_date
```

This makes the information easier to use in subsequent workflow nodes.

---

## 3. Message a Model

Google Gemini analyzes the student's profile.

The AI is instructed to provide:

- Career recommendations
- Skill gaps
- Next steps

The expected response format is JSON so that it can be processed programmatically.

---

## 4. Code in JavaScript

The JavaScript node extracts the Gemini response and converts it into structured data.

The resulting fields are:

```text
career_recommendations
skill_gaps
next_steps
```

These values are then passed to the Google Sheets and Gmail nodes.

---

## 5. Append Row in Sheet

The generated information is stored in Google Sheets.

This creates a simple database of submitted profiles and AI-generated recommendations.

---

## 6. Send a Message

Finally, the system sends the recommendation results to the email address submitted by the student.

This completes the automated process without requiring manual intervention.

---

# 🧪 Example Use Case

A student submits:

```text
Education: Undergraduate

Skills:
Java, HTML, CSS, SQL

Interests:
Technology, AI, Finance

Preferred Industry:
FinTech

Career Goal:
Work in a technology-driven finance role
```

The AI analyzes the profile and may return structured recommendations such as:

```text
Career Recommendations:
• FinTech Software Engineer
• Data Analyst
• Quantitative Developer

Skill Gaps:
• Python
• Data Structures & Algorithms
• Statistics
• Financial Markets

Next Steps:
• Build a finance-related software project
• Strengthen DSA fundamentals
• Learn financial markets
• Practice data analysis
```

The generated information is then:

**Stored in Google Sheets → Sent to the student's email**

---

# 🔐 Security

This repository is designed to keep authentication information private.

### Never commit:

```text
API keys
OAuth tokens
Passwords
Private credentials
.env files
Private webhook URLs
Private database credentials
```

The GitHub version of the workflow removes n8n credential objects and replaces private spreadsheet configuration with placeholders.

Before publishing your own workflow, always inspect the exported JSON for sensitive information.

---

# ⚠️ Important Configuration

The workflow contains a placeholder for the Google Sheet configuration:

```text
YOUR_GOOGLE_SHEET_ID
```

Replace it with your own Google Sheet ID after importing the workflow.

Do not publish a private production spreadsheet identifier or credentials if you want the repository to remain fully sanitized.

---

# 🧩 Troubleshooting

### Gemini node does not run

Check that:

- Your Gemini credentials are connected.
- The selected Gemini model is available in your n8n environment.
- The model node is receiving the expected form data.

### Google Sheets node fails

Check that:

- Your Google account is connected.
- The spreadsheet exists.
- The selected sheet has the expected columns.
- Your n8n Google Sheets credential has the required permissions.

### Email is not sent

Check that:

- Gmail credentials are connected.
- The submitted email address is valid.
- The Gmail node is correctly mapped to the form's email field.

### AI output is empty or malformed

The JavaScript node expects the Gemini response to contain text in the expected response structure.

If the Gemini response format changes, inspect the output of the **Message a model** node and update the JavaScript parser accordingly.

---

# 🔮 Future Improvements

Possible upgrades for this project include:

- 📈 Career recommendation scoring
- 📚 Personalized learning-roadmap generation
- 🔎 Job-role matching
- 💼 Job-board API integration
- 📊 Career analytics dashboard
- 🧠 Improved AI prompt engineering
- 🗃️ Database integration
- 🔐 User authentication
- 🌐 Dedicated web application frontend
- 📄 Resume analysis
- 🎓 Course and certification recommendations
- 📬 Follow-up career emails
- 📅 Automated career-progress tracking

---

# 🎯 Project Goals

This project demonstrates practical experience with:

- AI automation
- Workflow design
- API-based integrations
- Prompt engineering
- JavaScript data processing
- Structured JSON
- Google Workspace automation
- Email automation
- No-code/low-code development
- Building an end-to-end AI application

It is designed as a portfolio project showing how multiple services can be connected into a single automated AI workflow.

---

# 👩‍💻 Author

**Tanushree P**

BTech Computer Science Engineering Student  
CVR College of Engineering  
Graduating in 2028

---

# 📄 License

This project is intended for educational and portfolio purposes.

You are free to adapt the workflow for your own learning and projects. If you publish a modified version, consider crediting the original project.

---

## ⭐ Support the Project

If you found this project useful, consider giving the repository a ⭐ on GitHub.

**Built with n8n + Gemini + Google Sheets + Gmail 🚀**
