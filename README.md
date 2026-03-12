# Clyvara Rework
New and improved Clyvara website — Fall 2025 release.

Clyvara is an AI-powered platform designed to help generate structured anesthesia care plans for medical students and clinicians. The system leverages a modern web architecture with a React frontend, FastAPI backend, and a PostgreSQL database, alongside retrieval-augmented generation (RAG) powered by AWS Bedrock.

---

# ⚙️ Setup

## 1. Create and activate a virtual environment
```bash
python -m venv <env_name>
source <env_name>/bin/activate
```

## 2. Install dependencies
```bash
pip install -r requirements.txt
```

## 3. Configure backend environment variables
Create a `.env` file in `/backend` and add your API and database credentials:

```
OPENAI_API_KEY="your_secret_key_here"
DATABASE_URL="your_database_url_here"
```

## 4. Configure frontend environment variables
Create a `.env.local` file in `/frontend`:

```
VITE_SUPABASE_URL="supabase_url_here"
VITE_SUPABASE_ANON_KEY="your_secret_key_here"
```

---

# Development Workflow

## Create a new feature branch
```bash
git checkout -b <branch_name>
```

## Run the app locally

Run **backend** and **frontend** separately.

### Backend
```bash
uvicorn main:app --reload
```

### Frontend
```bash
npm run dev
```

---

# 🏗 Architecture Overview

Clyvara follows a **three-layer architecture** consisting of a frontend client, backend API server, and database layer.

## Frontend
**React**

The frontend renders the user interface and handles user interaction. It communicates with the backend through API requests.

Responsibilities include:

- Rendering the interface for medical students
- Collecting user inputs for anesthesia planning
- Displaying generated AI care plans
- Managing client-side state and navigation

---

## Backend
**FastAPI**

The backend acts as the orchestration layer of the system. It processes requests from the frontend, manages business logic, interacts with the database, and communicates with AWS Bedrock for AI-powered generation.

Responsibilities include:

- Handling API endpoints
- Managing the retrieval-augmented generation pipeline
- Querying stored medical knowledge
- Generating anesthesia care plans using LLMs
- Managing authentication and user data

---

## Database
**PostgreSQL**

PostgreSQL is used as the relational database for persistent storage.

Stored data includes:

- User accounts
- Saved care plans
- Structured medical references
- System metadata

---

## Retrieval Augmented Generation (RAG)
**AWS Bedrock**

Clyvara uses retrieval-augmented generation to improve the reliability of AI-generated care plans.

RAG pipeline:

1. A user submits a query (e.g., patient condition or procedure).
2. The backend retrieves relevant medical context from stored knowledge.
3. This context is passed to an LLM through AWS Bedrock.
4. The model generates a structured anesthesia care plan grounded in retrieved information.

This approach reduces hallucinations and improves medical accuracy by grounding the model in curated data.

---

# 🧠 Design Decisions

## React Frontend

React was chosen for several reasons:

### User Accessibility
The interface is designed to be simple and intuitive so that medical students of any technical background can easily navigate the platform.

### Reusable Components
React allows the creation of reusable UI components, which keeps the codebase organized and reduces duplication.

### Dynamic Interfaces
React’s client-side rendering allows UI elements to update without reloading the entire page, providing a smoother experience when interacting with generated plans.

### Maintainability
The component-based architecture results in cleaner code structure and easier long-term maintenance.

---

## FastAPI Backend

FastAPI was selected as the backend framework for several reasons:

### Fast Development
FastAPI allows rapid API development with clear routing and automatic validation using Python type hints.

### Python Ecosystem
Since most AI tooling and machine learning libraries are Python-based, FastAPI integrates naturally with LLM workflows and data processing.

### Performance
FastAPI is built on ASGI and handles concurrent requests efficiently, allowing the system to scale without large increases in latency.

### Built-in Documentation
FastAPI automatically generates interactive API documentation using OpenAPI and Swagger.

---

# 🧩 Notes

- Make sure both backend and frontend servers are running for full functionality.
- Commit changes only from feature branches and open a PR to merge into `main`.
- Use the `.env.example` format (if present) for consistent environment setup.
