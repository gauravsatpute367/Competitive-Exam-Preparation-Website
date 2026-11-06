# Competitive Exam — Preparation dashboard

A responsive, standalone competitive-exam dashboard with a daily study plan, interactive quiz, subject-filtered question practice, answer explanations, searchable resources, exam selection, and a quick question-solver preview.

## Run it with live AI

The live tutor needs Python 3 and an API key from an OpenAI-compatible chat-completions provider. The provider may require a paid account. The key stays on the server and is never sent to the browser.

1. In PowerShell, go to this project folder and create your private settings file:

```powershell
Copy-Item .env.example .env
notepad .env
```

2. Put your own provider key after `OPENAI_API_KEY=` in `.env`, then save. Do not include surrounding quotes.
3. If the server is already running, refresh the dashboard. Otherwise start it:

```powershell
python server.py
```

4. Open `http://127.0.0.1:8000` and confirm the tutor shows **Live AI ready**.

The server reads `.env` for each AI request, and shell environment variables take precedence. If you use another compatible provider, set `OPENAI_BASE_URL` to its API base URL and `OPENAI_MODEL` to a model available to your account in `.env`.

Without a configured key, the dashboard still opens and reports that live AI is unavailable. The chat displays setup, network, and provider errors instead of quietly substituting canned answers. If you see `403 Forbidden` or an HTML response, open the site through `http://127.0.0.1:8000` rather than opening `index.html` directly; a static hosting service must explicitly proxy/allow `/api/health` and `/api/chat` to the Python server.

## Features and demo notes

- Study-plan checkboxes, target exam, question count, and theme preference are saved in browser local storage.
- The sign-in form is a session-only UI preview. It does not create accounts, authenticate users, or send/store credentials.
- The question library contains original, illustrative practice questions—not verified or official previous-year exam questions. Add a verified question corpus, licensing review, and answer keys before presenting items as official past papers.
- The question solver sends the conversation to the configured AI provider through the local server. Provider usage may incur charges and follows the provider’s data policies. Avoid sending sensitive personal information.
- Exam countdowns and performance figures are illustrative placeholders; connect a trusted exam calendar and learner data source before using them as real schedules or analytics.

`server.py` is a local development server bound to `127.0.0.1`. It blocks requests for `.env` files. Do not expose it directly to the internet; a public deployment needs a production web server, authentication, rate limiting, and provider-side usage controls.
