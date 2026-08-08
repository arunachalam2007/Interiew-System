# InterviewAce AI - Production AI-Powered Personalized Interview Preparation System

**InterviewAce AI** is an enterprise-grade, full-stack AI platform designed to empower candidates to master technical, system design, behavioral, and coding interviews. It features real-time AI mock evaluations, multi-language sandboxed code execution, ATS resume parsing, FAISS vector memory retrieval, personalized 30/60/90-day learning roadmaps, and an administrative control suite.

---

## 🚀 Complete System Sitemap & Feature Matrix

| Module | Features & Capabilities | Route |
| :--- | :--- | :--- |
| **Landing Page** | High-converting hero, live interactive AI demo, features matrix, social proof | `/` |
| **Authentication** | JWT double-token flow, Google OAuth sign-in, password reset recovery | `/login`, `/signup`, `/forgot-password` |
| **Dashboard** | Readiness gauge, recent sessions, quick mock launch modal, performance overview | `/dashboard` |
| **Company Mock Room** | FAANG tracks (Google, Meta, Amazon, Apple, Netflix, Uber), STAR evaluation, voice mode | `/mock-room` |
| **Coding Platform** | Multi-language code runner (Python, JS, C, C++, Java), DSA catalog, AI Big-O complexity review | `/coding` |
| **AI Chat Assistant** | ChatGPT-style interface, prompt presets, thread search, speech-to-text / text-to-speech | `/ai-chat` |
| **ATS Resume Analyzer** | PDF parser, ATS match score (0-100), missing keywords, actionable suggestions | `/resume-analyzer` |
| **Analytics & Readiness** | 7-Day active streak heatmap, skill radar, coding stats, unlocked achievements & badges | `/analytics` |
| **30/60/90 Roadmap** | Personalized phased learning plan with interactive milestone checkboxes | `/roadmap` |
| **Calendar & Reminders** | Scheduled mock sessions grid & notifications feed with filter tabs | `/calendar` |
| **Admin Control Suite** | User management CRUD, Question catalog CRUD, Company track CRUD, Feedback reports | `/admin` |

---

## 🏗️ Architecture Layout

```
interview-system/
├── backend/
│   ├── app/
│   │   ├── api/v1/endpoints/   # Auth, Users, Interviews, Resume, AI Interview, Roadmap, Coding, Chat, Analytics, Notifications, Admin
│   │   ├── core/               # Config, Database, Security, Celery App, Logging
│   │   ├── models/             # SQLAlchemy 2.0 Async Models (User, Session, QuestionResponse)
│   │   ├── repositories/       # Repository Pattern (BaseRepository, UserRepository, InterviewRepository)
│   │   ├── schemas/            # Pydantic v2 validation models
│   │   ├── services/           # AuthService, UserService, AIService, ResumeService, LangChainAIService, CodeExecutorService, CodeAIService, ChatAssistantService, AnalyticsService, AdminService
│   │   ├── tasks/              # Celery background tasks
│   │   └── main.py             # FastAPI entry point with CORS, exception handlers & security headers
│   ├── tests/                  # Pytest unit & integration test suite
│   ├── Dockerfile
│   └── requirements.txt
├── frontend/
│   ├── src/
│   │   ├── components/         # Common UI primitives, Layouts, Route guards
│   │   ├── context/            # AuthContext, ThemeContext
│   │   ├── lib/                # Axios API client with automatic token refresh
│   │   ├── pages/              # Landing, Login, Signup, ForgotPassword, Dashboard, Profile, Settings, Practice, ResumeAnalyzer, MockInterviewRoom, LearningRoadmap, CodingPlatform, AIChatAssistant, Analytics, CalendarNotifications, AdminDashboard
│   │   ├── services/           # Auth, User, Interview, Resume, AIInterview, Roadmap, Coding, Chat, Analytics, Notifications, Admin services
│   │   ├── types/              # Complete TypeScript definitions
│   │   ├── App.tsx             # React Router 6 setup
│   │   └── main.tsx            # Vite entry point
│   ├── Dockerfile
│   └── package.json
├── nginx/
│   └── nginx.conf              # Nginx Reverse Proxy & SSL headers
├── .github/
│   └── workflows/
│       └── ci-cd.yml          # GitHub Actions CI/CD Pipeline
├── docker-compose.yml         # Postgres, Redis, Backend, Celery, Nginx Frontend
├── .env.example
└── README.md
```

---

## 🛠️ Quick Start & Local Execution

### Option 1: Docker Compose (Recommended)

Run the full stack with single command:

```bash
docker-compose up --build
```

- **Frontend Application**: [http://localhost](http://localhost) (or [http://localhost:5173](http://localhost:5173))
- **FastAPI Backend API**: [http://localhost:8000](http://localhost:8000)
- **Interactive OpenAPI Documentation**: [http://localhost:8000/docs](http://localhost:8000/docs)

---

### Option 2: Manual Local Development Setup

#### Backend Setup
```bash
cd backend
python -m venv .venv
source .venv/bin/activate  # On Windows: .venv\Scripts\activate
pip install -r requirements.txt
uvicorn app.main:app --reload --port 8000
```

#### Run Pytest Unit & Integration Tests
```bash
cd backend
pytest -v
```

#### Frontend Setup
```bash
cd frontend
npm install
npm run dev
```

---

## 🌐 Enterprise Deployment Guide

### Deploying to Cloud (AWS EC2 / DigitalOcean / GCP)

1. Provision a Cloud Virtual Machine (Ubuntu 22.04 LTS).
2. Install Docker and Docker Compose.
3. Clone repository and setup production environment variables:
   ```bash
   cp .env.example .env
   # Edit .env with production database credentials, SECRET_KEY, and OpenAI API Key
   ```
4. Build and start containers in detached mode:
   ```bash
   docker-compose -f docker-compose.yml up -d --build
   ```
5. Obtain SSL Certificate via Certbot:
   ```bash
   sudo apt-get install certbot python3-certbot-nginx
   sudo certbot --nginx -d yourdomain.com
   ```

---

## 🔒 Security Specifications

- **Token Security**: Standard Bearer JWT Access tokens (60 min expiration) + Refresh tokens (7 days) with HTTP interceptor auto-renewal.
- **Password Security**: Bcrypt hashing via PassLib context.
- **Protection Headers**: Strict Content-Security-Policy, X-Frame-Options (`DENY`), X-Content-Type-Options (`nosniff`).
- **Input Validation**: Pydantic v2 strict schema enforcement.
