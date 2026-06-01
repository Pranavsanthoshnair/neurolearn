# NeuroLearn AI

An accessible, learning-focused study assistant aimed at helping students learn with clear explanations, quizzes, and text extraction from images. The project is especially oriented toward supportive, step-by-step learning for neurodivergent learners (ADHD, dyslexia, autism).

> **Repository status:** This repository currently ships **standalone HTML prototypes**. A full FastAPI + React stack is described in older documentation and in `docker-compose.yml`, but **`backend/`, `frontend/`, and `ml/` are not present in this tree yet.** See [Roadmap](#roadmap) for the intended architecture.

## Table of contents

- [Overview](#overview)
- [What's in this repo](#whats-in-this-repo)
- [Features](#features)
- [Tech stack](#tech-stack)
- [Project structure](#project-structure)
- [Installation](#installation)
- [Usage](#usage)
- [Screenshots](#screenshots)
- [Configuration](#configuration)
- [Docker Compose (planned stack)](#docker-compose-planned-stack)
- [Roadmap](#roadmap)
- [Contributing](#contributing)
- [License](#license)

## Overview

NeuroLearn AI provides study assistance through browser-based demos:

1. **`neurolearn_offline.html`** — Works without a backend. Uses a built-in knowledge base, local math/quiz logic, and browser OCR (Tesseract.js).
2. **`offline_study_chatbot.html`** — **StudyBot** UI that calls the Anthropic Messages API for richer, mode-based tutoring (requires internet and API access).

## What's in this repo

| Artifact | Description |
|----------|-------------|
| `neurolearn_offline.html` | Offline-first study assistant + OCR (no server required) |
| `offline_study_chatbot.html` | StudyBot chat UI with multiple study modes (online LLM) |
| `docker-compose.yml` | Compose file for a **planned** FastAPI + React setup (not runnable until those folders exist) |
| `.gitignore` | Ignores paths for the planned Python/React/ML layout |

## Features

### Offline demo (`neurolearn_offline.html`)

- **Study chatbot** with modes: Explain, Math, Quiz, Clean notes
- **Built-in explanations** for: photosynthesis, gravity, Newton's first law, democracy, mitosis, water cycle, how the heart works
- **Math helper**: linear equations (e.g. `2x + 5 = 15`) and basic arithmetic expressions
- **Quizzes** for: photosynthesis, water cycle
- **OCR tab**: upload or drag-and-drop images (JPG, PNG, WEBP, BMP); extract text with Tesseract.js
- **Send OCR text to chatbot** to structure/clean notes
- **Quick-ask chips** for common topics
- **Offline badge** in UI — core chat logic runs without a backend (OCR engine loads from CDN on first use)

### StudyBot demo (`offline_study_chatbot.html`)

- **Modes**: Explain, Quiz Me, Summarise, Formulas, Flashcards, Examples
- **Suggestion chips** that change per mode
- **Subject detection** (e.g. Maths, Biology, Physics) from your question text
- **Conversation history** in the current session
- **Clear** button to reset the chat
- Uses the **Anthropic Messages API** (`claude-sonnet-4-20250514` in source)

> **Note:** The StudyBot file does not include API authentication headers in the current source. You will need to add a secure API key flow (or a backend proxy) before it can return real model responses. Do not commit API keys to the repository.

## Tech stack

| Layer | Technology |
|-------|------------|
| UI | HTML, CSS, JavaScript (no build step) |
| Offline OCR | [Tesseract.js](https://github.com/naptha/tesseract.js) (loaded from jsDelivr CDN) |
| Online tutor | Anthropic Messages API (StudyBot demo only) |
| Planned (not in repo) | FastAPI backend, React frontend, Firebase, ML training — see `docker-compose.yml` and `.gitignore` |

## Project structure

```
neurolearn/
├── .gitignore
├── README.md
├── docker-compose.yml           # Planned backend + frontend (folders not included yet)
├── neurolearn_offline.html      # Offline study assistant + OCR
└── offline_study_chatbot.html   # StudyBot (online LLM client)
```

## Installation

### Prerequisites

- A modern web browser (Chrome, Firefox, Edge, or Safari)
- **For offline demo:** optional internet on **first load** to download Tesseract.js from the CDN
- **For StudyBot demo:** internet access and a valid Anthropic API setup (see [Configuration](#configuration))

### Clone the repository

```bash
git clone https://github.com/Pranavsanthoshnair/neurolearn.git
cd neurolearn
```

### Run locally (recommended)

Serving files over HTTP avoids some browser restrictions on `file://` URLs and external scripts.

**Python 3:**

```bash
python -m http.server 8080
```

Then open:

- http://localhost:8080/neurolearn_offline.html
- http://localhost:8080/offline_study_chatbot.html

**Windows (PowerShell), same directory:**

```powershell
python -m http.server 8080
```

### Open without a local server

You can also open the `.html` files directly in your browser (double-click or **File → Open**). If OCR or API calls fail, use the HTTP server method above.

## Usage

### Offline demo (`neurolearn_offline.html`)

1. Open the file in your browser.
2. **Study Chatbot** tab:
   - Choose a mode pill (Explain, Math, Quiz, Clean notes).
   - Type a question or click a suggestion chip.
   - Press **Enter** to send (Shift+Enter for a new line).
3. **OCR** tab:
   - Upload or drag an image with clear printed text.
   - Click **Extract text from image**.
   - Copy the result or **Send to chatbot to explain**.

**Topics with full built-in answers:** photosynthesis, gravity, Newton's laws, democracy, mitosis, water cycle, heart.

**Quiz command examples:** `Quiz me on photosynthesis`, `Quiz me on water cycle`.

### StudyBot demo (`offline_study_chatbot.html`)

1. Configure Anthropic API access (see Configuration).
2. Open the file in your browser.
3. Select a mode (Explain, Quiz Me, etc.).
4. Click a suggestion chip or type your question.
5. Use **Clear** to reset the conversation.

## Screenshots

Screenshots are not included in the repository yet. Suggested captures for a future PR:

| Screenshot | File | What to show |
|------------|------|----------------|
| Offline chat | `neurolearn_offline.html` | Explain mode with a topic answer |
| OCR flow | `neurolearn_offline.html` | Image upload + extracted text |
| StudyBot modes | `offline_study_chatbot.html` | Mode bar + sample explanation |

Add images under `docs/images/` (create the folder) and link them here when available.

## Configuration

### Offline demo

| Item | Details |
|------|---------|
| Tesseract.js CDN | Loaded from `cdn.jsdelivr.net` on first OCR use |
| Language | OCR uses English (`eng`) in source |
| Offline use | Chat logic runs locally; OCR needs the CDN at least once unless you self-host `tesseract.min.js` |

### StudyBot demo

| Item | Details |
|------|---------|
| API endpoint | `https://api.anthropic.com/v1/messages` |
| Model | `claude-sonnet-4-20250514` (as in source) |
| API key | **Not wired in the current file** — implement `x-api-key` (or a backend proxy) before use; never commit secrets |

### Planned full-stack app (not in this repo)

When `backend/` and `frontend/` are added, environment variables may include:

**Backend (planned):**

```env
GEMINI_API_KEY=your_gemini_api_key
# Or: OPENAI_API_KEY=your_openai_key
FIREBASE_CREDENTIALS_PATH=./firebase-adminsdk.json
```

**Frontend (planned):**

```env
REACT_APP_API_URL=http://localhost:8000
REACT_APP_FIREBASE_API_KEY=your_key
REACT_APP_FIREBASE_AUTH_DOMAIN=your_project.firebaseapp.com
REACT_APP_FIREBASE_PROJECT_ID=your_project_id
REACT_APP_FIREBASE_STORAGE_BUCKET=your_project.appspot.com
REACT_APP_FIREBASE_MESSAGING_SENDER_ID=your_sender_id
REACT_APP_FIREBASE_APP_ID=your_app_id
```

## Docker Compose (planned stack)

`docker-compose.yml` defines a **planned** development setup:

- **backend** — FastAPI on port `8000` (build context `./backend`)
- **frontend** — React dev server on port `3000` (volume `./frontend`)

These services **will not start** until `backend/` and `frontend/` exist with their Dockerfiles and source code.

```bash
# Only after backend/ and frontend/ are added:
docker compose up --build
```

## Roadmap

Planned components (referenced in `.gitignore` and legacy docs, not yet in the repository):

- FastAPI backend with routers (simplify, quiz, OCR, translate, TTS, chat, emotion, focus, adaptive, dashboard)
- React frontend with Firebase Auth and Firestore gamification
- ML training (`ml/train_adaptive.py`)
- Accessibility settings (large font, high contrast, themes) in the web app

## Contributing

`CONTRIBUTING.md` is not in this repository yet. For **NSoC'26** contributions:

1. Check the issue tracker for "Improve and Expand README.md" (or your assigned issue).
2. Follow program-specific branch, commit, and PR rules from NSoC organizers.
3. Keep documentation aligned with **what is actually in the tree** — do not document features that are not implemented.

When `CONTRIBUTING.md` is added, follow it and link it here:

See [CONTRIBUTING.md](CONTRIBUTING.md) for details.

## License

No `LICENSE` file is present in this repository. Contact the maintainers before redistributing or using this code in production.
