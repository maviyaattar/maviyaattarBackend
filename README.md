# Portfolio Backend API + Quiz Platform

A unified Node.js + Express + MongoDB backend combining the portfolio API and full quiz platform.

## Features

### Portfolio API
- **Projects** – CRUD endpoints for portfolio projects
- **Contacts** – Contact form submission and management
- **Ameer AI** – Groq-powered AI chat assistant for the portfolio

### Quiz Platform
- **Auth** – Creator registration/login with JWT
- **Quiz Management** – Create, start, delete quizzes with unique codes
- **AI Quiz Generation** – Generate MCQ questions from a topic using Groq AI
- **Participant Flow** – Join quiz by code, fetch questions, submit answers
- **PDF Reports** – Auto-generated PDF result report on submission
- **Leaderboard & Summary** – Per-quiz leaderboard and statistics
- **Logo Upload** – Cloudinary-backed logo upload for quizzes

## Getting Started

### Prerequisites
- Node.js >= 18
- MongoDB instance

### Installation

```bash
npm install
```

### Configuration

Copy `.env.example` to `.env` and fill in values:

```bash
cp .env.example .env
```

| Variable | Required | Description |
|---|---|---|
| `PORT` | No (default 3000) | Server port |
| `MONGO_URI` | **Yes** | MongoDB connection string |
| `JWT_SECRET` | **Yes** | Secret for signing JWT tokens |
| `GROQ_API_KEY` | **Yes** | Groq API key (Ameer AI + quiz generation) |
| `CLOUDINARY_CLOUD_NAME` | Yes for logo uploads | Cloudinary cloud name |
| `CLOUDINARY_API_KEY` | Yes for logo uploads | Cloudinary API key |
| `CLOUDINARY_API_SECRET` | Yes for logo uploads | Cloudinary API secret |

### Running

```bash
# Production
npm start

# Development (with auto-restart)
npm run dev
```

## API Endpoints

### Portfolio

| Method | Path | Description |
|---|---|---|
| GET | `/` | Health check |
| GET | `/projects` | List all projects |
| POST | `/projects` | Create project |
| PUT | `/projects/:id` | Update project |
| DELETE | `/projects/:id` | Delete project |
| POST | `/contact` | Submit contact form |
| GET | `/contacts` | List all contacts |
| DELETE | `/contacts/:id` | Delete contact |
| POST | `/ai/chat` | Ameer AI chat |

### Auth

| Method | Path | Description |
|---|---|---|
| POST | `/api/auth/register` | Register quiz creator |
| POST | `/api/auth/login` | Login and receive JWT |
| GET | `/api/auth/me` | Get current user (auth required) |

### Quiz (Creator – auth required)

| Method | Path | Description |
|---|---|---|
| POST | `/api/quiz/create` | Create a new quiz |
| POST | `/api/quiz/generate-ai` | AI-generate MCQ questions |
| GET | `/api/quiz/my` | List creator's quizzes |
| GET | `/api/quiz/:code` | Get quiz details |
| POST | `/api/quiz/start/:code` | Start (go live) a quiz |
| DELETE | `/api/quiz/delete/:code` | Delete quiz and submissions |
| GET | `/api/quiz/participants/:code` | List participants |
| GET | `/api/quiz/participant-pdf/:code/:rollNo` | Download participant PDF |
| POST | `/api/upload-logo` | Upload quiz logo to Cloudinary |

### Quiz (Participant – public)

| Method | Path | Description |
|---|---|---|
| POST | `/api/quiz/join/:code` | Check if quiz is joinable |
| GET | `/api/quiz/questions/:code` | Fetch questions for live quiz |
| POST | `/api/quiz/submit/:code` | Submit answers (returns PDF) |
| GET | `/api/quiz/leaderboard/:code` | Get leaderboard |
| GET | `/api/quiz/summary/:code` | Get quiz statistics |
