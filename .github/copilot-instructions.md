# GitHub Copilot Instructions for OctoCAT Supply Chain Demo

## Project Overview
This is a **GitHub Copilot demonstration project** showcasing Agent Mode, Vision, and MCP servers. The codebase consists of a FastAPI backend (`/api`) and React frontend (`/frontend`) designed to highlight Copilot's capabilities across different scenarios.

## GitHub Repo Information
This repo is hosted in GitHub:
- owner: kqh34
- repo: github-scaled-agent-mode-webinar-python

## Architecture & Key Patterns

### Backend (FastAPI + Python)
- **Entry Points**: `api/main.py` (dev wrapper) → `api/app/main.py` (FastAPI app)
- **Route Pattern**: Each entity has matching `/models/{entity}.py` and `/routes/{entity}.py` files
- **Data Storage**: In-memory lists with seed data from `api/app/seed_data.py` (no database)
- **API Convention**: RESTful endpoints at `/api/{entity-plural}` with full CRUD operations
- **Testing**: pytest with FastAPI TestClient, coverage reporting via `pytest.ini`

### Frontend (React + TypeScript)
- **Build Tool**: Vite with Tailwind CSS
- **API Integration**: Centralized config in `src/api/config.ts` with Codespace auto-detection
- **Routing**: React Router with main routes: `/`, `/products`, `/admin/products`, `/about`, `/login`
- **Context Pattern**: `AuthContext` and `ThemeContext` for global state
- **Component Structure**: `/components/entity/{entity}/` for domain-specific components

### Development Workflow
- **Quick Start**: `npm run dev` (starts both API on :3000 and frontend on :5173)
- **Build Command**: `npm run build` (builds both workspaces)
- **Testing**: `npm run test` (runs both API pytest and frontend vitest)

## Code Review & Quality Guidelines

When generating suggestions:

- **Prefer incremental, minimal diffs**: Preserve existing style and naming conventions
- **Prioritize critical issues**: Surface security, correctness, and data integrity issues before micro-optimizations
- **Enforce type safety**: Avoid `any` unless justified. Suggest adding/refining model or DTO types when gaps appear
- **Reduce duplication**: Flag duplicate logic that belongs in a shared utility or repository method
- **Consistent error handling**: Use FastAPI's HTTPException with appropriate status codes. Follow existing patterns in `/api/app/routes/`
- **Test coverage**: Request unit tests for new route logic and React Testing Library coverage for critical UI paths
- **Performance awareness**: Highlight unnecessary data loading or large bundle additions (this demo uses in-memory data, so N+1 queries aren't applicable)
- **Configuration management**: Prefer environment variable driven configuration; avoid hard-coded paths/secrets
