# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A caffeine beverage tierlist website where users can find and rank caffeine drinks.

## Planned Tech Stack

- **Frontend**: React
- **Backend**: FastAPI (Python)
- **Database**: MySQL
- **Deploy**: AWS

## Development Setup

> Update this section as the project is scaffolded.

### Frontend (React)
```bash
cd frontend
npm install
npm run dev      # start dev server
npm run build    # production build
npm run lint     # lint
npm test         # run tests
```

### Backend (FastAPI)
```bash
cd backend
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
uvicorn main:app --reload   # start dev server
pytest                      # run tests
```

## Architecture

> Fill in once the project structure is established.

The app is expected to follow a client-server architecture:
- React SPA communicates with FastAPI via REST (or similar)
- FastAPI handles business logic and talks to MySQL
- Deployed on AWS (expected: frontend on S3/CloudFront, backend on EC2/ECS/Lambda)
