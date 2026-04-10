# Landit

**AI-powered career command center for macOS**

Landit finds jobs from 7+ sources, scores them against your resume, runs live AI mock interviews, tracks your pipeline, and coaches you to the offer. All from one native Mac app. 100% local — your data never leaves your machine.

[![Download](https://img.shields.io/github/v/release/humancto/landit-releases?label=Download&style=for-the-badge&color=4A9EFF)](https://github.com/humancto/landit-releases/releases/latest)
[![macOS](https://img.shields.io/badge/macOS-14%2B-black?style=for-the-badge&logo=apple)](https://github.com/humancto/landit-releases/releases/latest)
[![License](https://img.shields.io/badge/license-proprietary-gray?style=for-the-badge)](https://github.com/humancto/landit-releases)

---

![Landit Dashboard](screenshots/dashboard.png)

## Features

### Job Discovery

Search 7+ sources simultaneously — Indeed, LinkedIn, Greenhouse, Lever, Ashby, RemoteOK, Hacker News, Adzuna, and more. Every job is AI-scored 0-100 against your resume so the best matches rise to the top.

![Jobs](screenshots/jobs.png)

### Live AI Mock Interviews

Practice with a real-time AI interviewer powered by Gemini Live API. Choose text, audio, or audio+video mode. Get scored on communication, problem solving, technical skills, and cultural fit.

![Interview Practice](screenshots/practice.png)

### Pipeline Tracking

Kanban board to manage applications from discovery to offer. Track status, follow-up dates, interview rounds, contacts, and compare multiple offers side by side.

![Pipeline](screenshots/pipeline.png)

### Career Coach

24/7 AI career mentor that knows your profile, interview history, and job preferences. Ask about strategy, salary negotiation, resume tips, or career direction.

![Career Coach](screenshots/coach.png)

### Discovery Configuration

Configure 8 job sources with per-company slug support for Greenhouse, Lever, and Ashby. Role typeahead with 500+ roles across 20 domains.

![Discovery Sources](screenshots/discovery.png)

### Interview Analytics

Track performance over time with score trends, category breakdowns, and areas to improve. See exactly where you're getting better.

![Analytics](screenshots/analytics.png)

### Multi-Provider AI

Plug in any provider — Google Gemini, OpenAI, Anthropic, or Groq. Keys stored securely in macOS Keychain. Switch models per feature (fast scoring vs deep analysis).

![Settings](screenshots/settings.png)

## All Features

| Module              | What it does                                                 |
| ------------------- | ------------------------------------------------------------ |
| **Job Discovery**   | 7+ source aggregation, AI scoring, dedup, location filtering |
| **Live Interviews** | Voice + video mock interviews via Gemini Live API            |
| **Text Interviews** | Behavioral, technical, system design, coding practice        |
| **Career Coach**    | AI chat with full context of your profile and history        |
| **Pipeline**        | Kanban board with status tracking and drag-and-drop          |
| **Contacts**        | Networking CRM with company association                      |
| **Follow-ups**      | Ghost detection, automated reminders                         |
| **Offers**          | Side-by-side offer comparison                                |
| **Resume**          | Import, extract, AI analysis and rewriting                   |
| **Cover Letter**    | AI-generated per job with skill gap analysis                 |
| **Answer Vault**    | Save and reuse common application answers                    |
| **Notes**           | Prep notes tied to applications                              |
| **Documents**       | File management for contracts, references                    |
| **AI Analysis**     | LinkedIn profile and contract analysis                       |
| **Market Data**     | Salary benchmarks and market trends                          |
| **Analytics**       | Interview performance tracking over time                     |

## Download

1. Grab the latest `.dmg` from [Releases](https://github.com/humancto/landit-releases/releases/latest)
2. Open the DMG and drag **Landit.app** to **Applications**
3. Launch Landit — the onboarding wizard walks you through setup
4. Add your AI API key in Settings (Google Gemini recommended for live interviews)

### System Requirements

- macOS 14.0 (Sonoma) or later
- Apple Silicon or Intel Mac
- Python 3.8+ (optional, for enhanced job discovery via JobSpy)

### AI Provider Setup

Landit is BYOK (bring your own key). Get a free API key from any supported provider:

| Provider                                            | Get Key             | Best For                            |
| --------------------------------------------------- | ------------------- | ----------------------------------- |
| [Google Gemini](https://aistudio.google.com/apikey) | Free tier available | Live voice interviews, fast scoring |
| [OpenAI](https://platform.openai.com/api-keys)      | Pay-as-you-go       | Deep analysis, cover letters        |
| [Anthropic](https://console.anthropic.com/)         | Pay-as-you-go       | Career coaching, resume review      |
| [Groq](https://console.groq.com/keys)               | Free tier available | Ultra-fast inference                |

## Privacy

- **100% local** — All data stored in SQLite on your Mac
- **No accounts required** — Download, open, use
- **No tracking** — Analytics is opt-in and anonymous
- **Your keys, your data** — API keys stored in macOS Keychain, never sent anywhere except the provider
- **Open inspection** — No obfuscation, no phone-home

## Built by [HumanCTO](https://humancto.com)
