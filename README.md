# JARVIS AI

A GitHub-ready personal AI assistant starter built with Python, FastAPI, the OpenAI Responses API, SQLite conversation memory, and a simple browser interface.

## Current features

- Conversational AI through the OpenAI API.
- Persistent conversation history stored locally in SQLite.
- Optional web search through the Responses API web search tool.
- Browser speech input where supported by the browser.
- Browser text-to-speech for reading the latest response.
- Separate session IDs and a memory-clearing API endpoint.
- API key kept on the server in an environment file.

## Requirements

- Python 3.10+
- An OpenAI API key and API billing/usage access.
- Internet connection for model requests and optional web search.

## Run locally

### Windows PowerShell

```powershell
git clone https://github.com/YOUR-USERNAME/jarvis-ai.git
cd jarvis-ai
py -m venv .venv
.venv\Scripts\Activate.ps1
pip install -r requirements.txt
Copy-Item .env.example .env
notepad .env
```

Add your API key to `.env`, save it, then run:

```powershell
uvicorn main:app --reload
```

### macOS / Linux

```bash
git clone https://github.com/YOUR-USERNAME/jarvis-ai.git
cd jarvis-ai
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
cp .env.example .env
```

Add your API key to `.env`, then run:

```bash
uvicorn main:app --reload
```

Open http://127.0.0.1:8000 in your browser.

## Publish to GitHub

Create an empty GitHub repository named `jarvis-ai`, then:

```bash
git init
git add .
git commit -m "Initial JARVIS AI assistant"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/jarvis-ai.git
git push -u origin main
```

Never commit `.env` or paste your API key into source code. `.gitignore` excludes `.env` and the local database.

## API endpoints

- `GET /health` — health check.
- `POST /chat` — send a message.
- `DELETE /memory/{session_id}` — clear a session's stored conversation.

Example request:

```json
{
  "message": "Explain how solar panels work.",
  "session_id": "my-session",
  "use_web_search": true
}
```

## Important security notes

This is a foundation, not a fully autonomous computer operator. It does not currently execute terminal commands, access personal accounts, send emails, or control smart-home devices. Keep it that way until each capability has authentication, narrow permissions, audit logs, and explicit confirmation for consequential actions.

For a public deployment, add user authentication, rate limiting, HTTPS, request-size limits, database encryption/backups, and per-user data isolation. Do not expose this development server directly to the public internet.

## Roadmap

1. Add authenticated user profiles and memory controls.
2. Add a proper live voice agent using the current OpenAI voice/realtime stack.
3. Add carefully permissioned tools (calendar, email, files, smart-home).
4. Add a desktop app and a wake-word option.
5. Add tests, logging, monitoring, and deployment automation.

## Architecture

```text
Browser UI
   |
   v
FastAPI backend ---- OpenAI Responses API
   |                         |
   v                         v
SQLite memory             AI reasoning
                             |
                             v
                         Web search
```
