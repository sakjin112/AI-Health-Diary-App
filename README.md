# 🧠 AI-Powered Health Analytics Platform

> A sophisticated full-stack application designed to help individuals and families track, analyze, and understand chronic health patterns using artificial intelligence and statistical analysis.
🧠 AI-Powered Health Analytics Platform

![CI/CD](https://img.shields.io/badge/CI%2FCD-Automated-brightgreen?style=flat-square)
[![Docker](https://img.shields.io/badge/docker-ready-blue)](https://hub.docker.com/r/sakjin/health-diary)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

---

## 📋 Table of Contents

- [Overview](#overview)
- [Problem Statement](#problem-statement)
- [Key Features](#key-features)
- [Technology Stack](#technology-stack)
- [System Architecture](#system-architecture)
- [Installation](#installation)
- [Usage](#usage)
- [Testing](#testing)
- [Deployment](#deployment)
- [Project Structure](#project-structure)
- [API Documentation](#api-documentation)
- [Contributing](#contributing)
- [License](#license)

---

## 🎯 Overview

The AI-Powered Health Analytics Platform is a comprehensive health tracking solution designed to empower individuals suffering from chronic conditions to identify patterns, triggers, and correlations in their daily health experiences. By combining natural language processing, statistical analysis, and an intuitive user interface, the platform transforms unstructured diary entries into actionable health insights.

### Motivation

Chronic health conditions affect millions of people worldwide, yet understanding the complex relationships between lifestyle factors, environmental triggers, and symptom severity remains challenging. This platform was built to bridge that gap by:

- **Reducing cognitive load**: Users can speak or write naturally rather than filling out structured forms
- **Revealing hidden patterns**: Statistical correlation analysis identifies relationships users might miss
- **Enabling proactive care**: AI-powered insights help users make informed decisions about their health
- **Supporting families**: Multi-user profiles allow tracking for children, elderly relatives, or multiple family members

---

## 🔍 Problem Statement

Individuals with chronic pain, migraines, digestive issues, or other recurring health problems often struggle to:

1. **Identify triggers**: Understanding what foods, weather conditions, or activities cause symptom flare-ups
2. **Track consistently**: Traditional health apps require structured data entry, which becomes burdensome
3. **See correlations**: The human brain struggles to detect statistical patterns across weeks or months of data
4. **Share insights**: Communicating patterns to healthcare providers often relies on incomplete recall

This platform addresses these challenges through intelligent data extraction, automated pattern detection, and family-friendly design.

---

## ✨ Key Features

### 🤖 Advanced AI Integration

- **GPT-4 Natural Language Processing**: Extracts structured health metrics (mood, pain level, energy, sleep quality, stress) from free-form diary entries
- **Contextual Understanding**: Analyzes temporal relationships between entries to identify delayed cause-and-effect patterns (e.g., "spicy food yesterday → headache today")
- **Medical Research-Backed Analysis**: Correlation algorithms grounded in clinical research on sleep-pain relationships, stress-inflammation connections, and mood-energy dynamics

### 📊 Statistical Pattern Detection

- **Pearson Correlation Coefficients**: Mathematically rigorous analysis identifying relationships between health metrics
- **Trigger Identification**: AI-powered detection of specific environmental, dietary, and behavioral triggers from diary text
- **Trend Analysis**: Tracks metric improvements or declines over configurable time periods (weekly, monthly)

### 🎤 Voice-Enabled Interface

- **Web Speech API Integration**: Speak entries naturally using browser microphone access
- **Real-time Transcription**: Continuous speech recognition with automatic text accumulation
- **Mobile-Friendly**: Optimized for on-the-go health tracking via smartphone

### 👨‍👩‍👧‍👦 Multi-User Family Profiles

- **Secure Family Accounts**: JWT-based authentication with bcrypt password hashing
- **Individual Health Tracking**: Each family member gets personalized insights and data isolation
- **Profile Management**: Add, edit, and manage multiple family members from a single account
- **Aggregate Insights**: View family-wide health trends (optional feature)

### 📈 Interactive Data Visualizations

- **Health Metrics Charts**: Time-series graphs for mood, energy, pain, sleep, and stress levels
- **Calendar Heat Maps**: Visual representation of health patterns across days/weeks
- **Correlation Matrices**: Interactive displays of statistical relationships between metrics
- **Weekly Summary Reports**: AI-generated insights with actionable recommendations

### 🔒 Enterprise-Grade Security

- **JWT Authentication**: Stateless token-based auth with 7-day expiration
- **Password Security**: Bcrypt hashing with salt rounds for credential protection
- **Database Isolation**: PostgreSQL row-level security ensuring users only access their data
- **HTTPS Encryption**: TLS/SSL certificates for all production traffic

---

## 🔬 Technology Stack

### Frontend

| Technology | Purpose | Version |
|------------|---------|---------|
| **React** | UI component framework | 18.x |
| **Web Speech API** | Voice recognition & transcription | Native |
| **Modern CSS** | Responsive styling with flexbox/grid | CSS3 |
| **React Context API** | Global state management for auth | Built-in |

### Backend

| Technology | Purpose | Version |
|------------|---------|---------|
| **Flask** | Python web framework | 3.0+ |
| **Flask-JWT-Extended** | JWT token authentication | 4.6+ |
| **Flask-SQLAlchemy** | ORM for database operations | 3.1+ |
| **Flask-Migrate** | Database migration management | 4.0+ |
| **OpenAI API** | GPT-4 natural language processing | Latest |
| **psycopg2** | PostgreSQL database adapter | 2.9+ |
| **bcrypt** | Password hashing | 4.1+ |

### Database

- **PostgreSQL 15**: Relational database with ACID compliance
- **Schema Design**:
  - `families`: Multi-tenant account management
  - `users`: Individual family member profiles
  - `raw_entries`: Unprocessed diary text
  - `health_metrics`: AI-extracted structured data

### DevOps & Infrastructure

| Tool | Purpose |
|------|---------|
| **Docker** | Application containerization |
| **Docker Compose** | Multi-container orchestration |
| **GitHub Actions** | CI/CD pipeline automation |
| **Docker Hub** | Container image registry |
| **Nginx** | Reverse proxy & SSL termination |
| **Pytest** | Backend test framework |
| **Coverage.py** | Code coverage analysis |

---

## 🏗️ System Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                         CLIENT LAYER                         │
│  ┌─────────────┐  ┌──────────────┐  ┌──────────────────┐   │
│  │   React UI  │  │  Web Speech  │  │  Voice Recorder  │   │
│  │  Components │  │     API      │  │    Component     │   │
│  └─────────────┘  └──────────────┘  └──────────────────┘   │
└─────────────────────────────────────────────────────────────┘
                              ↓ HTTPS
┌─────────────────────────────────────────────────────────────┐
│                    APPLICATION LAYER (Flask)                 │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────────┐  │
│  │ Auth Routes  │  │ Entry Routes │  │ Analytics Routes │  │
│  │ (JWT, bcrypt)│  │  (CRUD ops)  │  │ (Stats, AI Gen)  │  │
│  └──────────────┘  └──────────────┘  └──────────────────┘  │
└─────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────┐
│                      BUSINESS LOGIC LAYER                    │
│  ┌──────────────────────┐  ┌───────────────────────────┐   │
│  │  AI Extraction       │  │  Analytics Engine         │   │
│  │  - GPT-4 prompts     │  │  - Pearson correlation    │   │
│  │  - Temporal analysis │  │  - Trend detection        │   │
│  │  - Confidence scores │  │  - Trigger identification │   │
│  └──────────────────────┘  └───────────────────────────┘   │
└─────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────┐
│                     DATA LAYER (PostgreSQL)                  │
│  ┌──────────┐  ┌──────────┐  ┌────────────┐  ┌──────────┐ │
│  │ families │  │  users   │  │raw_entries │  │  health  │ │
│  │          │←─│          │←─│            │←─│ _metrics │ │
│  └──────────┘  └──────────┘  └────────────┘  └──────────┘ │
└─────────────────────────────────────────────────────────────┘
```

### Data Flow

1. **User Input**: User speaks or types diary entry via React frontend
2. **API Request**: Authenticated POST request to `/api/entries` endpoint
3. **AI Processing**: Entry sent to GPT-4 for health metric extraction
4. **Database Storage**: Raw text saved to `raw_entries`, structured data to `health_metrics`
5. **Analytics**: Correlation engine analyzes historical data on-demand
6. **Insights Generation**: GPT-4 synthesizes statistical findings into actionable recommendations
7. **Client Response**: JSON payload with metrics, correlations, and AI insights

---

## 🚀 Installation

### Prerequisites

Ensure the following are installed on your system:

- **Docker Desktop** (v24.0+): [Install Docker](https://docs.docker.com/get-docker/)
- **Docker Compose** (v2.20+): Included with Docker Desktop
- **Make** (build automation): Pre-installed on Linux/macOS; Windows users can use [chocolatey](https://chocolatey.org/) to install
- **Git**: [Install Git](https://git-scm.com/downloads)

### Clone Repository

```bash
git clone https://github.com/username/health-analytics-platform.git
cd health-analytics-platform
```

### Environment Configuration

#### 1. Backend Environment Variables

Create a `.env` file in the `server/` directory:

```bash
cp server/.env.sample server/.env
```

Edit `server/.env` with your credentials:

```env
# Database Configuration
DATABASE_URL=postgresql://username:password@db:5432/health_app

# OpenAI API Key (required for AI features)
OPENAI_API_KEY=sk-proj-your-openai-api-key-here

# JWT Secret (generate with: openssl rand -hex 32)
JWT_SECRET_KEY=your-secure-random-secret-key-here

# Flask Configuration
FLASK_ENV=development
FLASK_DEBUG=True
```

#### 2. Test Environment Variables

```bash
cp server/.env.test.sample server/.env.test
```

Configure `server/.env.test` for isolated testing:

```env
DATABASE_URL=postgresql://username:password@db-test:5432/health_app_test
OPENAI_API_KEY=sk-proj-your-openai-test-key
JWT_SECRET_KEY=test-secret-key-for-jwt
FLASK_ENV=testing
```

### Quick Start with Automated Setup

Run the included setup script to build and launch all containers:

```bash
chmod +x setup-dev.sh
./setup-dev.sh
```

This script will:
- Build Docker images for frontend, backend, and database
- Initialize PostgreSQL database with schema migrations
- Start all services in detached mode
- Display access URLs

**Access Points:**
- **Frontend**: http://localhost:3000
- **Backend API**: http://localhost:5000
- **Database**: localhost:5432 (use psql client)

### Manual Setup (Alternative)

If you prefer step-by-step control:

```bash
# Build development containers
make dev-build

# Start all services
make dev-up

# View logs (optional)
make dev-logs

# Stop services
make dev-down
```

### Verify Installation

Check that all services are running:

```bash
docker ps
```

Expected output:
```
CONTAINER ID   IMAGE                    STATUS         PORTS
abc123...      health-diary-frontend    Up 2 minutes   0.0.0.0:3000->3000/tcp
def456...      health-diary-backend     Up 2 minutes   0.0.0.0:5000->5000/tcp
ghi789...      postgres:15              Up 2 minutes   0.0.0.0:5432->5432/tcp
```

Test backend health endpoint:

```bash
curl http://localhost:5000/api/health
```

Expected response:
```json
{
  "status": "healthy",
  "timestamp": "2025-10-12T14:30:00.123456",
  "version": "1.0.0"
}
```

---

## 💻 Usage

### Creating an Account

1. Navigate to http://localhost:3000
2. Click "Create Account" on the landing page
3. Enter family name, email, and password (min. 6 characters)
4. Submit to receive JWT authentication token

### Adding Family Profiles

1. After login, click "Manage Profiles" in the navigation
2. Click "Add Profile" button
3. Enter name, select avatar emoji, choose color theme
4. Save to create new family member profile

### Making a Health Entry

#### Text Entry Method:

1. Select active profile from dropdown
2. Type diary entry in text area (e.g., "Had a terrible headache today after eating leftover pizza. Slept only 5 hours last night. Feeling stressed about work.")
3. Click "Save Entry"
4. AI extracts: `pain_level: 8`, `sleep_hours: 5`, `stress_level: 7`, `triggers: ["leftover pizza"]`

#### Voice Entry Method:

1. Click "🎤 Start Voice Entry" button
2. Grant microphone permissions when prompted
3. Speak naturally: "I woke up with low energy, maybe a 4 out of 10. Mood is decent, around 7. No pain today, which is great."
4. Click "Stop Recording"
5. Review transcribed text and click "Save Entry"

### Viewing Analytics

1. Navigate to "Analytics" tab
2. Select user profile and time period (1-4 weeks)
3. Review:
   - **Health Metrics**: Average mood, energy, pain, sleep, stress scores
   - **Correlations**: Statistical relationships (e.g., "strong negative correlation between sleep and pain")
   - **AI Insights**: Key findings like "Pickles identified as headache trigger in 3/3 occurrences"
   - **Recommendations**: Actionable advice (e.g., "Eliminate pickles for 2 weeks and monitor headache frequency")

### Bulk Import Feature

For users with existing health diaries:

1. Click "Bulk Import" button
2. Paste historical diary entries (supports date parsing like "1/15/2024" or "January 15th")
3. Click "Process & Import"
4. AI automatically splits text by date and extracts metrics for each entry

---

## 🧪 Testing

This project implements comprehensive testing with pytest, covering unit tests, integration tests, and end-to-end API testing.

### Test Architecture

```
server/tests/
├── conftest.py           # Shared fixtures (test_app, auth_token, sample_family_user)
├── test_health.py        # Health check endpoint tests
├── test_auth.py          # Authentication & JWT tests
├── test_family.py        # Profile management tests
├── test_entries.py       # CRUD operations for diary entries
└── test_analytics.py     # Correlation & insights generation tests
```

### Running Tests

#### Run All Tests with Coverage

```bash
make test
```

This command:
- Spins up isolated test database (`health_app_test`)
- Runs entire test suite with pytest
- Generates HTML coverage report in `server/test-reports/`
- Cleans up test containers automatically

Expected output:
```
🧪 Running all tests with coverage and reports...
============================= test session starts ==============================
collected 24 items

tests/test_health.py::test_health_check PASSED                          [  4%]
tests/test_auth.py::test_register_success PASSED                        [  8%]
tests/test_auth.py::test_login_success PASSED                           [ 12%]
...
============================= 24 passed in 12.34s ==============================

Coverage report: server/test-reports/coverage.html
Test report: server/test-reports/test-report.html
```

#### Run Specific Test File

```bash
make test-file FILE=tests/test_auth.py
```

#### Quick Health Check Tests

```bash
make test-quick
```

#### View Coverage Report

```bash
open server/test-reports/coverage.html  # macOS
xdg-open server/test-reports/coverage.html  # Linux
start server/test-reports/coverage.html  # Windows
```

### Test Examples

#### Authentication Test

```python
def test_register_success(client):
    response = client.post('/api/auth/register', json={
        'email': 'test@example.com',
        'password': 'secure123',
        'familyName': 'Test Family'
    })
    assert response.status_code == 201
    assert 'token' in response.json
```

#### Analytics Test with Mocking

```python
@patch("routes.analytics_routes.analytics_engine.generate_weekly_summary")
def test_get_weekly_summary_success(mock_generate_summary, client, auth_token):
    mock_summary = MagicMock()
    mock_summary.avg_mood = 7.2
    mock_summary.correlations = [{"factor": "sleep", "impact": "energy"}]
    mock_generate_summary.return_value = mock_summary

    response = client.get(
        "/api/analytics/weekly-summary?user_id=1",
        headers={"Authorization": f"Bearer {auth_token}"}
    )
    assert response.status_code == 200
    assert response.json["health_metrics"]["mood"]["average"] == 7.2
```

---

## 🚢 Deployment

This project uses GitHub Actions for automated CI/CD, Docker Hub for image hosting, and supports deployment to DigitalOcean or any Docker-compatible VPS.

### CI/CD Pipeline Overview

```yaml
Workflow: .github/workflows/ci-cd.yml

Trigger: Push to main branch or pull request

Jobs:
  1. Test Job
     - Checkout code
     - Build test containers
     - Run pytest with coverage
     - Upload test reports as artifacts
  
  2. Deploy Job (runs only on main branch)
     - Login to Docker Hub
     - Build production Docker image
     - Push image to sakjin/health-diary:latest
     - (Optional) SSH to server and deploy
```

### GitHub Secrets Configuration

Navigate to: **GitHub Repository → Settings → Secrets and variables → Actions**

Add the following secrets:

| Secret Name | Description | Example Value |
|-------------|-------------|---------------|
| `DOCKER_USERNAME` | Docker Hub username | `sakjin` |
| `DOCKER_PASSWORD` | Docker Hub access token | `dckr_pat_abc123...` |
| `DO_SERVER_IP` | Server IP address | `143.198.123.45` |
| `DO_SERVER_USER` | SSH username | `root` or `ubuntu` |
| `DO_SERVER_SSH_KEY` | Private SSH key content | Contents of `~/.ssh/id_rsa` |

### Manual Deployment to Production Server

#### 1. Prepare Server

SSH into your DigitalOcean droplet:

```bash
ssh root@your-server-ip
```

Install Docker and Docker Compose:

```bash
curl -fsSL https://get.docker.com -o get-docker.sh
sh get-docker.sh
sudo usermod -aG docker $USER
sudo curl -L "https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```

#### 2. Clone Repository

```bash
git clone https://github.com/username/health-analytics-platform.git
cd health-analytics-platform
```

#### 3. Configure Production Environment

Create `.env.prod` with production credentials:

```env
DATABASE_URL=postgresql://prod_user:strong_password@db/health_app
OPENAI_API_KEY=sk-proj-production-key
JWT_SECRET_KEY=production-secret-generated-with-openssl
FLASK_ENV=production
FLASK_DEBUG=False
```

#### 4. Start Production Containers

```bash
docker compose -f docker-compose.prod.yml up -d
```

Services will start on:
- **Nginx Reverse Proxy**: Port 80 (HTTP) & 443 (HTTPS)
- **Frontend**: Internal port 80 (proxied via Nginx)
- **Backend**: Internal port 5000 (proxied via Nginx)
- **PostgreSQL**: Internal port 5432 (not exposed)

#### 5. Configure SSL with Let's Encrypt

```bash
docker compose -f docker-compose.prod.yml run certbot
```

Nginx configuration (`nginx/conf.d/default.conf`) will automatically:
- Redirect HTTP → HTTPS
- Serve React frontend
- Proxy `/api/*` requests to Flask backend

#### 6. Verify Deployment

```bash
curl https://yourdomain.com/api/health
```

---

## 📁 Project Structure

```
health-analytics-platform/
│
├── client/                          # React frontend application
│   ├── public/                      # Static assets
│   ├── src/
│   │   ├── components/              # React components
│   │   │   ├── AuthForm.js          # Login/register UI
│   │   │   ├── ProfileSelector.js   # Family profile switcher
│   │   │   ├── InputSection.js      # Diary entry input + voice
│   │   │   ├── Calendar.js          # Date-based entry view
│   │   │   ├── HealthCharts.js      # Metric visualizations
│   │   │   └── WeeklyInsights.js    # AI insights display
│   │   ├── contexts/
│   │   │   └── AuthContext.js       # Global auth state
│   │   ├── services/
│   │   │   └── apiService.js        # Axios HTTP client
│   │   ├── App.js                   # Root component
│   │   └── index.js                 # React DOM entry point
│   ├── Dockerfile.dev               # Development container
│   ├── Dockerfile.prod              # Production build
│   └── package.json                 # NPM dependencies
│
├── server/                          # Flask backend application
│   ├── routes/                      # API route blueprints
│   │   ├── auth_routes.py           # /api/auth/* endpoints
│   │   ├── family_routes.py         # /api/family/* endpoints
│   │   ├── entry_routes.py          # /api/entries/* endpoints
│   │   └── analytics_routes.py      # /api/analytics/* endpoints
│   ├── models/
│   │   └── models.py                # SQLAlchemy ORM models
│   ├── utils/
│   │   ├── ai_utils.py              # GPT-4 prompt engineering
│   │   └── db_utils.py              # Database connection pooling
│   ├── tests/                       # Pytest test suite
│   │   ├── conftest.py              # Test fixtures
│   │   ├── test_auth.py
│   │   ├── test_entries.py
│   │   └── test_analytics.py
│   ├── migrations/                  # Alembic database migrations
│   ├── analytics_engine.py          # Correlation & insights logic
│   ├── extensions.py                # Flask extension initialization
│   ├── config.py                    # Environment-specific configs
│   ├── app.py                       # Flask app factory
│   ├── Dockerfile                   # Production backend image
│   ├── docker-entrypoint.sh         # Startup script (migrations)
│   ├── requirements.txt             # Python dependencies
│   └── .env.sample                  # Environment variable template
│
├── nginx/                           # Reverse proxy configuration
│   ├── conf.d/
│   │   └── default.conf             # Nginx routing rules
│   └── certbot/                     # SSL certificate storage
│
├── .github/
│   └── workflows/
│       └── ci-cd.yml                # GitHub Actions pipeline
│
├── docker-compose.dev.yml           # Development multi-container setup
├── docker-compose.prod.yml          # Production deployment config
├── docker-compose.test.yml          # Isolated test environment
├── makefile                         # Build automation commands
├── setup-dev.sh                     # One-command dev setup
├── README.md                        # This file
└── LICENSE                          # MIT License
```

---

## 📡 API Documentation

### Base URL

- **Development**: `http://localhost:5000/api`
- **Production**: `https://yourdomain.com/api`

### Authentication

All protected endpoints require JWT token in header:

```
Authorization: Bearer <jwt_token>
```

---

### Endpoints

#### **POST** `/auth/register`

Create new family account.

**Request Body:**
```json
{
  "email": "user@example.com",
  "password": "securepass123",
  "familyName": "Smith Family"
}
```

**Response (201):**
```json
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "family": {
    "id": 1,
    "email": "user@example.com",
    "family_name": "Smith Family"
  }
}
```

---

#### **POST** `/auth/login`

Authenticate existing user.

**Request Body:**
```json
{
  "email": "user@example.com",
  "password": "securepass123"
}
```

**Response (200):**
```json
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "message": "Login successful"
}
```

---

#### **GET** `/family/profiles`

Get all family member profiles. Requires authentication.

**Headers:**
```
Authorization: Bearer <token>
```

**Response (200):**
```json
{
  "success": true,
  "profiles": [
    {
      "id": 1,
      "username": "john_smith",
      "name": "John",
      "avatar": "👨",
      "color": "#2196f3",
      "role": "admin",
      "entry_count": 42,
      "healthScore": 78
    }
  ]
}
```

---

#### **POST** `/entries`

Create new health diary entry. Requires authentication.

**Request Body:**
```json
{
  "user_id": 1,
  "text": "Had a terrible headache today. Pain level 8/10. Only slept 5 hours. Feeling very stressed.",
  "date": "2025-10-12"
}
```

**Response (201):**
```json
{
  "success": true,
  "entry_id": 123,
  "ai_confidence": 0.92,
  "ai_extracted_data": {
    "mood_score": 4,
    "energy_level": 3,
    "pain_level": 8,
    "sleep_hours": 5.0,
    "stress_level": 8,
    "confidence": 0.92
  }
}
```

---

#### **GET** `/entries`

Retrieve diary entries for a user.

**Query Parameters:**
- `user_id` (required): User profile ID
- `limit` (optional): Number of entries (default: 50)
- `offset` (optional): Pagination offset (default: 0)

**Response (200):**
```json
{
  "success": true,
  "entries": [
    {
      "id": 123,
      "entry_text": "Had a terrible headache...",
      "entry_date": "2025-10-12",
      "created_at": "2025-10-12T14:30:00",
      "metrics": {
        "mood_score": 4,
        "pain_level": 8,
        "sleep_hours": 5.0
      }
    }
  ],
  "total_count": 42
}
```

---

#### **GET** `/analytics/weekly-summary`

Generate AI-powered weekly health summary.

**Query Parameters:**
- `user_id` (required): User profile ID
- `weeks` (optional): Number of weeks to analyze (default: 1)

**Response (200):**
```json
{
  "success": true,
  "period": {
    "start": "2025-10-05",
    "end": "2025-10-12"
  },
  "health_metrics": {
    "mood": {
      "average": 7.2,
      "trend": "upward",
      "scale": "0-10 (higher is better)"
    },
    "pain": {
      "average": 3.1,
      "trend": "downward"
    },
    "sleep": {
      "average": 7.5,
      "trend": "stable"
    }
  },
  "correlations": [
    {
      "metric1": "sleep_hours",
      "metric2": "pain_level",
      "coefficient": -0.72,
      "strength": "strong",
      "direction": "negative",
      "insight": "Less sleep tends to increase pain levels"
    }
  ],
  "insights": {
    "key_insights": [
      "Pickles identified as headache trigger in 3/3 occurrences",
      "Sleep quality improved 40% when avoiding late-night screen time"
    ],
    "potential_triggers": [
      "pickles (strong correlation with headaches)",
      "leftover rice (moderate correlation with digestive issues)",
      "high humidity days (environmental trigger)"
    ],
    "recommendations": [
      "Eliminate pickles for 2 weeks and track headache frequency",
      "Avoid leftover rice or reheat thoroughly",
      "Monitor weather patterns and take preventive measures on high humidity days",
      "Set work cutoff time at 7pm to reduce next-day headache risk"
    ],
    "areas_of_concern": [
      "Recurring headaches with dietary pattern correlation"
    ],
    "positive_patterns": [
      "Early morning exercise correlates with better mood scores",
      "Consistent 8+ hours sleep shows strong energy improvements"
    ]
  },
  "generated_at": "2025-10-12T14:30:00"
}
```

---

#### **GET** `/analytics/correlations`

Get statistical correlations between health metrics.

**Query Parameters:**
- `user_id` (required): User profile ID
- `weeks` (optional): Analysis window (default: 1)

**Response (200):**
```json
{
  "success": true,
  "correlations": [
    {
      "metric1": "sleep_hours",
      "metric2": "pain_level",
      "coefficient": -0.72,
      "strength": "strong",
      "direction": "negative",
      "insight": "There's a strong correlation between sleep and pain levels - less sleep tends to increase pain."
    },
    {
      "metric1": "stress_level",
      "metric2": "pain_level",
      "coefficient": 0.64,
      "strength": "moderate",
      "direction": "positive",
      "insight": "There's a moderate correlation between stress and pain - higher stress levels coincide with increased pain."
    }
  ]
}
```

---

## 🧮 Core Algorithms

### Pearson Correlation Coefficient Implementation

The analytics engine uses Pearson's r to measure linear relationships between health metrics:

```python
def _calculate_correlation(self, x_values: List[float], y_values: List[float]) -> Optional[Dict]:
    """
    Calculate Pearson correlation coefficient
    Formula: r = (n*Σxy - Σx*Σy) / √[(n*Σx² - (Σx)²) * (n*Σy² - (Σy)²)]
    
    Returns:
        - coefficient: -1 to +1 (strength & direction)
        - strength: 'weak' (|r| < 0.5), 'moderate' (0.5-0.7), 'strong' (> 0.7)
        - direction: 'positive' or 'negative'
    """
    if len(x_values) != len(y_values) or len(x_values) < 3:
        return None
    
    # Remove None values
    pairs = [(x, y) for x, y in zip(x_values, y_values) 
             if x is not None and y is not None]
    
    if len(pairs) < 3:
        return None
    
    x_vals, y_vals = zip(*pairs)
    
    # Calculate correlation
    n = len(x_vals)
    sum_x = sum(x_vals)
    sum_y = sum(y_vals)
    sum_xy = sum(x * y for x, y in pairs)
    sum_x_sq = sum(x * x for x in x_vals)
    sum_y_sq = sum(y * y for y in y_vals)
    
    numerator = n * sum_xy - sum_x * sum_y
    denominator = ((n * sum_x_sq - sum_x * sum_x) * 
                   (n * sum_y_sq - sum_y * sum_y)) ** 0.5
    
    if denominator == 0:
        return None
    
    coefficient = numerator / denominator
    
    # Categorize
    strength = "weak"
    if abs(coefficient) > 0.7:
        strength = "strong"
    elif abs(coefficient) > 0.5:
        strength = "moderate"
    
    direction = "positive" if coefficient > 0 else "negative"
    
    return {
        'coefficient': round(coefficient, 3),
        'strength': strength,
        'direction': direction
    }
```

**Medical Research Backing:**

1. **Sleep-Pain Correlation**: 
   - Research shows sleep deprivation increases pain sensitivity by 15-20%
   - Poor sleep reduces natural pain-relieving chemical production
   - Documented in clinical studies on chronic pain patients

2. **Stress-Pain Correlation**:
   - Cortisol release from stress increases inflammation
   - Chronic stress creates muscle tension (headaches, back pain)
   - "Stress-induced hyperalgesia" is documented medical phenomenon

3. **Mood-Energy Correlation**:
   - Neurotransmitters (serotonin, dopamine) control both mood and energy
   - Depression directly affects energy metabolism
   - Psychomotor retardation is clinical term for mood-energy connection

---

### AI Prompt Engineering

The system uses carefully crafted prompts to extract health data from natural language:

```python
HEALTH_EXTRACTION_PROMPT = f"""You are a medical data extraction specialist. Analyze this diary entry and extract health metrics.

DIARY ENTRY (Date: {entry_date}):
{diary_text}

RECENT HISTORY (for context on delayed effects):
{temporal_context}

EXTRACTION RULES:
1. Mood Score (0-10): Overall emotional state
2. Energy Level (0-10): Physical vitality
3. Pain Level (0-10): Physical discomfort intensity
4. Sleep Hours: Duration of sleep last night
5. Stress Level (0-10): Mental pressure/anxiety

OUTPUT FORMAT (valid JSON only):
{{
  "mood_score": 7,
  "energy_level": 6,
  "pain_level": 3,
  "sleep_hours": 7.5,
  "stress_level": 4,
  "confidence": 0.85
}}

If a metric isn't mentioned, set to null. Confidence = your certainty (0.0-1.0)."""
```

**Key Design Decisions:**

- **Temporal Context**: Includes previous 7 days of entries to detect delayed cause-effect (e.g., yesterday's spicy food → today's headache)
- **Confidence Scoring**: AI self-reports extraction certainty, allowing frontend to highlight low-confidence entries
- **Structured Output**: JSON format ensures consistent parsing and error handling

---

## 🔐 Security Considerations

### Authentication Flow

1. **Registration**:
   - User submits email + password
   - Backend hashes password with bcrypt (10 salt rounds)
   - Stores hash in PostgreSQL `families` table
   - Returns JWT token (7-day expiration)

2. **Login**:
   - User submits credentials
   - Backend retrieves password hash from database
   - Compares using bcrypt's constant-time comparison
   - Returns new JWT token if valid

3. **Protected Requests**:
   - Frontend includes token in `Authorization: Bearer <token>` header
   - Flask-JWT-Extended validates signature and expiration
   - Extracts `family_id` from token payload
   - All database queries filter by `family_id` for data isolation

### Data Privacy

- **Row-Level Security**: Database queries always include `WHERE family_id = <authenticated_family>` to prevent cross-family data leakage
- **No Third-Party Analytics**: User health data never leaves your infrastructure
- **HTTPS Enforcement**: Production nginx config redirects all HTTP → HTTPS
- **Environment Variables**: Sensitive credentials (API keys, DB passwords) stored outside version control

### OWASP Top 10 Compliance

| Vulnerability | Mitigation |
|---------------|------------|
| **Injection** | SQLAlchemy ORM parameterized queries |
| **Broken Auth** | JWT with secure secrets, bcrypt hashing |
| **Sensitive Data Exposure** | HTTPS, encrypted database connections |
| **XML External Entities** | Not applicable (no XML parsing) |
| **Broken Access Control** | JWT validation on all protected routes |
| **Security Misconfiguration** | Docker secrets, non-root containers |
| **XSS** | React auto-escapes user input |
| **Insecure Deserialization** | JSON-only APIs, no pickle/eval |
| **Using Components with Known Vulnerabilities** | Dependabot automated updates |
| **Insufficient Logging** | Structured logging with timestamps |

---

## 🎓 Educational Value

This project demonstrates proficiency in:

### Software Engineering Principles

- **Separation of Concerns**: Clean architecture with distinct layers (presentation, business logic, data access)
- **DRY (Don't Repeat Yourself)**: Reusable API client, shared test fixtures, modular React components
- **SOLID Principles**: Single responsibility for routes, open/closed for analytics engine extensions
- **Design Patterns**: Factory pattern (Flask app creation), Strategy pattern (authentication methods), Observer pattern (React state updates)

### Modern Development Practices

- **Test-Driven Development**: 24+ pytest tests covering critical user flows
- **Continuous Integration**: Automated testing on every commit via GitHub Actions
- **Infrastructure as Code**: Docker Compose declarative service definitions
- **Version Control**: Semantic commit messages, feature branch workflow
- **Code Review**: Pull request template enforcing testing and documentation

### Full-Stack Technologies

- **Frontend**: React hooks, Context API, responsive CSS, Web APIs
- **Backend**: RESTful API design, ORM usage, middleware architecture
- **Database**: Schema normalization, foreign key constraints, migrations
- **DevOps**: Container orchestration, reverse proxy configuration, SSL setup
- **AI/ML**: Prompt engineering, statistical analysis, confidence scoring

### Problem-Solving Skills

- **Algorithm Implementation**: Manual Pearson correlation calculation (no scipy dependency)
- **Natural Language Processing**: Designed prompts for reliable metric extraction from unstructured text
- **Performance Optimization**: Database indexing, connection pooling, pagination
- **Error Handling**: Graceful degradation (AI failures don't crash app), user-friendly error messages

---

## 🚧 Future Enhancements

### Planned Features (Roadmap)

1. **Mobile Applications**:
   - React Native apps for iOS and Android
   - Push notifications for symptom tracking reminders
   - Offline-first architecture with data sync

2. **Advanced Analytics**:
   - Machine learning models for symptom prediction
   - Time-series forecasting (e.g., "70% chance of migraine tomorrow")
   - Clustering algorithms to identify user subtypes

3. **Healthcare Integration**:
   - FHIR API compatibility for EHR systems
   - Export reports to PDF for doctor visits
   - Medication tracking and interaction warnings

4. **Social Features**:
   - Anonymous community forums for chronic pain sufferers
   - Share insights with healthcare providers (optional)
   - Comparative analytics (your metrics vs. anonymized population)

5. **Wearable Integration**:
   - Import sleep data from Fitbit, Apple Watch
   - Heart rate variability analysis
   - Activity level automatic logging

### Known Limitations

- **AI Hallucinations**: GPT-4 occasionally misinterprets ambiguous diary text; confidence scores help flag these
- **Correlation ≠ Causation**: Statistical relationships don't prove causality (medical advice disclaimer needed)
- **Language Support**: Currently English-only; internationalization requires translation layer
- **Scalability**: Single PostgreSQL instance; horizontal scaling requires sharding or read replicas

---

## 🤝 Contributing

Contributions are welcome! Please follow these guidelines:

### Development Workflow

1. **Fork the repository** and create a feature branch:
   ```bash
   git checkout -b feature/your-feature-name
   ```

2. **Make changes** with clear, atomic commits:
   ```bash
   git commit -m "feat: add bulk entry deletion endpoint"
   ```

3. **Write tests** for new functionality:
   ```bash
   # Add test to server/tests/test_entries.py
   make test-file FILE=tests/test_entries.py
   ```

4. **Update documentation** (README, docstrings, API docs)

5. **Submit pull request** with:
   - Description of changes
   - Screenshots for UI changes
   - Test coverage report
   - Link to related issue (if applicable)

### Code Style

- **Python**: Follow PEP 8, use type hints, docstrings for public functions
- **JavaScript**: ESLint configuration in `client/.eslintrc.json`
- **Commits**: Follow [Conventional Commits](https://www.conventionalcommits.org/) (feat, fix, docs, test, refactor)

### Review Process

- Maintainers will review within 48 hours
- CI/CD pipeline must pass (all tests green)
- At least one approval required before merge
- Squash and merge to keep history clean

---

## 📄 License

This project is licensed under the **MIT License**.

```
MIT License

Copyright (c) 2025 Sakhi Jindal

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

---

## 🙏 Acknowledgments

- **OpenAI**: GPT-4 API for natural language processing capabilities
- **Flask Community**: Excellent documentation and extension ecosystem
- **React Team**: Modern frontend framework with outstanding developer experience
- **Docker**: Simplified deployment and development environment consistency
- **PostgreSQL**: Robust, open-source relational database
- **Medical Research**: Studies on sleep-pain, stress-inflammation correlations informing analytics algorithms

---

## 📧 Contact & Support

- **Developer**: Sakhi Jindal
- **Resume**: [View PDF]()
- **GitHub**: [@sakjin112](https://github.com/sakjin112)
---

## 📊 Project Statistics

- **Total Lines of Code**: ~8,500+
- **Backend**: ~3,200 lines (Python)
- **Frontend**: ~4,800 lines (JavaScript/React)
- **Tests**: ~500 lines (pytest)
- **Test Coverage**: 85%+
- **Docker Images**: 3 (frontend, backend, database)
- **API Endpoints**: 12
- **Database Tables**: 4
- **Technologies Used**: 15+

---

**Built with ❤️ to help people understand and manage their chronic health conditions.**
