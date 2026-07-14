# 📱 Litera-AI Monorepo (Mobile & Services)

[![Flutter](https://img.shields.io/badge/Flutter-3.x-blue?style=for-the-badge&logo=flutter)](https://flutter.dev/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.100+-green?style=for-the-badge&logo=fastapi)](https://fastapi.tiangolo.com/)
[![Python](https://img.shields.io/badge/Python-3.10+-blue?style=for-the-badge&logo=python)](https://www.python.org/)
[![Docker](https://img.shields.io/badge/Docker-Enabled-blue?style=for-the-badge&logo=docker)](https://www.docker.com/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-Active-blue?style=for-the-badge&logo=postgresql)](https://www.postgresql.org/)

> **LITERA-AI App** is the core monorepo hosting the mobile application, high-performance FastAPI backend, and custom predictive AI algorithms for the Adaptive Literacy platform.

---

## 📂 Workspace Structure

```text
apps/
  ├── mobile/         # Flutter mobile application (Android & iOS)
  ├── backend/        # Python FastAPI backend service
  └── ai/             # DDA decision models and knowledge tracing engine
docs/                 # Visual diagrams, wireframes, and design specs
infra/                # Docker configuration, Nginx setup, CI/CD scripts
```

---

## ✨ Monorepo Features

- **📱 Flutter Mobile App**:
  - Implements Material 3 responsive styling and adaptive Dark/Light modes.
  - State management powered by **Riverpod** and robust routing with **GoRouter**.
  - **Offline-First Storage**: Cached locally using Hive, with an automated offline sync queue and connection status banner.
  - Complete workflow screens: Auth, diagnostic assessments, learning logs, profiles, and teacher dashboard monitors.

- **⚡ FastAPI Backend**:
  - Structured, asynchronous endpoints using SQLAlchemy and Alembic migrations.
  - Versioned API design (`/api/v1/...`).
  - Integrated with Redis for caching and rapid session management.

- **🤖 Predictive AI Module**:
  - Knowledge tracing calculations using student history data.
  - Dynamic Difficulty Adjustment (DDA) to recommend suitable literacy contents.

---

## 🚀 Setup & Execution Guide

### 📱 1. Mobile Application (Flutter)
```bash
cd apps/mobile
flutter pub get
flutter run
```

### ⚡ 2. Backend Server (FastAPI)
Create a `.env` in `apps/backend/` and configure:
```env
DATABASE_URL="postgresql+asyncpg://postgres:postgres@localhost:5432/litera_backend"
REDIS_URL="redis://localhost:6379/0"
```
Install dependencies and run:
```bash
cd apps/backend
python -m venv .venv
source .venv/bin/activate  # On Windows: .venv\Scripts\activate
pip install -e ".[dev]"
uvicorn app.main:app --reload
```

---

## 🛠️ Infrastructure & Deployment

You can stand up the entire system (Backend, Database, Cache) using Docker Compose:
```bash
cd infra/docker
docker-compose up -d
```
All traffic is routed smoothly through the Nginx reverse proxy configuration found in `infra/nginx/`.
