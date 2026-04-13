# 🧠 NeuroLearn AI

An accessible, AI-powered learning platform designed specifically for neurodivergent students (ADHD, Dyslexia, Autism).

---

## 📁 Folder Structure

```
neurolearn-ai/
├── backend/                  # FastAPI backend
│   ├── main.py               # Entry point
│   ├── requirements.txt
│   ├── routers/              # API route handlers
│   │   ├── simplify.py
│   │   ├── quiz.py
│   │   ├── ocr.py
│   │   ├── translate.py
│   │   ├── tts.py
│   │   ├── chat.py
│   │   ├── emotion.py
│   │   ├── focus.py
│   │   ├── adaptive.py
│   │   └── dashboard.py
│   ├── services/             # Business logic
│   │   ├── nlp_service.py
│   │   ├── ocr_service.py
│   │   ├── emotion_service.py
│   │   ├── focus_service.py
│   │   ├── tts_service.py
│   │   └── adaptive_service.py
│   ├── models/               # Pydantic models
│   │   └── schemas.py
│   └── utils/
│       └── firebase_admin.py
├── frontend/                 # React frontend
│   ├── public/
│   ├── src/
│   │   ├── components/       # Reusable UI components
│   │   ├── pages/            # Page-level components
│   │   ├── services/         # API + Firebase calls
│   │   ├── hooks/            # Custom React hooks
│   │   ├── context/          # React context (Auth, Theme)
│   │   └── utils/
│   ├── package.json
│   └── firebase.json
├── ml/
│   └── train_adaptive.py     # ML model training
└── README.md
```

---

## 🚀 Quick Start

### Backend

```bash
cd backend
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate
pip install -r requirements.txt
uvicorn main:app --reload --port 8000
```

### Frontend

```bash
cd frontend
npm install
npm start
```

---

## 🔧 Environment Variables

### Backend `.env`
```
GEMINI_API_KEY=your_gemini_api_key
# Or: OPENAI_API_KEY=your_openai_key
# Optional: custom Tesseract executable path for Windows
# TESSERACT_CMD=C:\Program Files\Tesseract-OCR\tesseract.exe
FIREBASE_CREDENTIALS_PATH=./firebase-adminsdk.json
```

### Frontend `.env`
```
REACT_APP_API_URL=http://localhost:8000
REACT_APP_FIREBASE_API_KEY=your_key
REACT_APP_FIREBASE_AUTH_DOMAIN=your_project.firebaseapp.com
REACT_APP_FIREBASE_PROJECT_ID=your_project_id
REACT_APP_FIREBASE_STORAGE_BUCKET=your_project.appspot.com
REACT_APP_FIREBASE_MESSAGING_SENDER_ID=your_sender_id
REACT_APP_FIREBASE_APP_ID=your_app_id
```

---

## 📦 Core Features

| Feature | Technology |
|---|---|
| Text Simplification | HuggingFace T5/BART |
| AI Quiz Generator | T5 QA Model |
| Handwriting OCR | OpenCV + Tesseract |
| Multilingual (Tamil) | Helsinki-NLP |
| Voice Chatbot | OpenAI + gTTS |
| Emotion Detection | DeepFace |
| Focus Detection | OpenCV Haar Cascade |
| Adaptive Learning | RandomForestClassifier |
| Gamification | Firebase Firestore |
| Auth | Firebase Auth |

---

## ☁️ Deployment

- **Frontend**: Firebase Hosting (`firebase deploy`)
- **Backend**: Render.com (connect GitHub repo) or AWS EC2

---

## ♿ Accessibility

- Large font mode
- High contrast mode
- Screen reader compatible
- Keyboard navigation
- Dark/Light theme toggle
