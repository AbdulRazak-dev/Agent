# 🤖 Nova AI Agent

Nova AI Agent is a lightweight **AI-powered voice assistant backend** built with Python and Flask.

It allows users to give natural-language commands and performs actions based on the command. The current version supports:

* 📧 AI-powered Gmail email generation
* ▶️ YouTube music search and playback
* 🎙️ Natural-language/voice-command integration
* 🔗 Automatic Gmail compose links
* 🌐 REST API endpoints
* 🚀 Deployment with Gunicorn

The project is designed to be extended with more AI-powered actions in the future.

---

## ✨ Features

### 📧 Gmail AI Agent

Nova can understand an email-related command and generate a professional email using Google's Gemini API.

For example:

```text
Write an email to john@example.com saying that I will attend the meeting tomorrow.
```

Nova extracts the recipient and sends the command to Gemini to generate:

* Email subject
* Professional email body
* Gmail compose URL

The generated Gmail URL can then be opened to continue editing and sending the email.

---

### ▶️ YouTube Agent

Nova can understand YouTube/music commands such as:

```text
Play Shape of You
```

or:

```text
Play song Believer
```

The agent searches YouTube, extracts a video ID, and generates an embeddable YouTube URL.

---

### 🎙️ Voice Command Ready

The backend is designed around commands supplied as text, making it suitable for integration with a browser-based speech-recognition interface.

A frontend can convert:

```text
🎙️ Voice
   ↓
📝 Speech-to-text
   ↓
🤖 Nova AI Agent
   ↓
⚡ Action
```

---

## 🏗️ Project Structure

```text
Agent/
│
├── app/
│   ├── __init__.py
│   │
│   ├── gmail/
│   │   ├── __init__.py
│   │   ├── gmail_gen.py
│   │   └── gmail_write.py
│   │
│   ├── youtube/
│   │   ├── __init__.py
│   │   └── play.py
│   │
│   └── templates/
│       └── index.html
│
├── requirements.txt
├── wsgi.py
└── README.md
```

---

## 🛠️ Tech Stack

| Technology | Purpose                   |
| ---------- | ------------------------- |
| Python     | Backend programming       |
| Flask      | Web framework and API     |
| Gemini API | AI email generation       |
| JavaScript | Frontend interaction      |
| HTML/CSS   | Nova AI interface         |
| YouTube    | Music/video search        |
| Gunicorn   | Production WSGI server    |
| Flask-CORS | Cross-origin API requests |

---

## 🔄 How It Works

### Gmail Flow

```text
User Command
     ↓
Nova AI
     ↓
Detect Gmail Command
     ↓
Extract Email Address
     ↓
Gemini AI
     ↓
Generate Subject + Body
     ↓
Create Gmail Compose URL
     ↓
Open Gmail
```

### YouTube Flow

```text
User Command
     ↓
Nova AI
     ↓
Detect Play Command
     ↓
Extract Song/Search Query
     ↓
Search YouTube
     ↓
Extract Video ID
     ↓
Generate YouTube Embed URL
     ↓
Play Video
```

---

# 📡 API Endpoints

## Health Check

### `GET /health`

Used to check whether the backend is running.

Example response:

```json
{
  "status": "ok",
  "service": "Nova AI Agent"
}
```

---

## Gmail Agent

### `POST /agent`

Processes an email command and generates a professional email using Gemini.

### Request

```json
{
  "command": "Write an email to john@example.com saying that I will attend the meeting tomorrow"
}
```

### Response

```json
{
  "success": true,
  "type": "email",
  "email_generated": true,
  "recipient": "john@example.com",
  "subject": "Meeting Attendance Confirmation",
  "body": "Dear John,\n\nI would like to confirm...",
  "gmail_url": "https://mail.google.com/..."
}
```

---

## YouTube Agent

### `POST /youtube/play`

Processes a YouTube/music command.

### Request

```json
{
  "command": "Play song Believer"
}
```

### Response

```json
{
  "success": true,
  "type": "youtube",
  "query": "Believer",
  "url": "https://www.youtube.com/embed/..."
}
```

---

# 🧠 Gmail Command Processing

Nova recognizes commands containing keywords such as:

```text
gmail
email
e-mail
mail
write an email
send an email
draft an email
compose an email
write mail
send mail
draft mail
compose mail
```

It also supports extracting an email address from natural speech.

For example:

```text
john@example.com
```

and:

```text
john at example dot com
```

can both be interpreted as:

```text
john@example.com
```

---

# 🤖 Gemini Integration

The Gmail agent uses the Gemini API to transform a user's command into a professional email.

The AI is instructed to:

* Keep the email natural and concise
* Avoid copying the command literally
* Avoid inventing information
* Generate an appropriate greeting
* Generate an appropriate closing
* Return a subject and body

The Gemini API key is loaded through an environment variable.

---

# 🔐 Environment Variables

Create your environment variables before running the application.

Example:

```env
Gemini_API_Key=your_gemini_api_key
```

Optional:

```env
GEMINI_MODEL=gemini-3.5-flash
CLIENT_EMAIL=your_client_email@example.com
```

> ⚠️ Never upload API keys or `.env` files containing secrets to GitHub.

---

# 🚀 Run Locally

## 1. Clone the repository

```bash
git clone https://github.com/AbdulRazak-dev/Agent.git
```

Move into the project:

```bash
cd Agent
```

---

## 2. Create a virtual environment

Windows:

```bash
python -m venv venv
```

Activate it:

```bash
venv\Scripts\activate
```

macOS/Linux:

```bash
python3 -m venv venv
source venv/bin/activate
```

---

## 3. Install dependencies

```bash
pip install -r requirements.txt
```

---

## 4. Configure API keys

Set your Gemini API key as an environment variable.

Windows PowerShell:

```powershell
$env:Gemini_API_Key="YOUR_API_KEY"
```

---

## 5. Start the application

```bash
python wsgi.py
```

The Flask application will start locally.

---

# ☁️ Deployment

The project can be deployed to platforms such as **Render** using Gunicorn.

### Build Command

```bash
pip install -r requirements.txt
```

### Start Command

```bash
gunicorn wsgi:app
```

The WSGI file exposes the Flask application as:

```python
app = create_app()
```

---

# 🔮 Future Improvements

Nova AI is designed to become a more capable personal AI assistant.

Possible future features include:

* 🎙️ Better voice recognition
* 🧠 Intent detection
* 💬 Conversational AI
* 📧 D
