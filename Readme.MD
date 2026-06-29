Currency Exchange Stock Management System

An internal management system for currency exchange bureaus. It lets you track currency balances, record buy and sell transactions, manage exchange rates, and ask an AI assistant operational questions in plain language.

Built with FastAPI, PostgreSQL, SQLAlchemy, Alembic, LangChain, Groq, and Docker.


What it does


Manage currencies (add, activate, deactivate)
Track physical stock balances per currency
Record buy and sell transactions with automatic stock updates
Manage exchange rates, synced daily from the European Central Bank
Ask the AI assistant things like "summarize today's activity" or "which currency has the highest balance"
Dashboard showing current balances, recent transactions, and daily volume



Requirements


Docker and Docker Compose
A Groq API key (free at console.groq.com) — only needed for the AI assistant



Running locally

Clone the repository and create a .env file:

cp .env.example .env

Open .env and fill in your values:

DATABASE_URL=keep it same
GROQ_API_KEY=your_groq_api_key_here
APP_ENV=development
APP_NAME=Currency Exchange System

Start everything with Docker:

docker-compose up --build

This starts PostgreSQL, runs database migrations automatically, seeds initial data, and starts the server.

Open the frontend by double-clicking frontend/index.html in your file explorer.

The API runs at http://localhost:8000 and the interactive API docs are at http://localhost:8000/docs.


Project structure

app/
  api/routes/      FastAPI routers — one file per module
  services/        Business logic — all rules live here
  models/          SQLAlchemy ORM models
  schemas/         Pydantic DTOs for request and response validation
  db/              Database session and connection
  ai/              LangChain + Groq assistant
  core/            Config, exceptions, background scheduler
alembic/           Database migrations
frontend/          Single HTML file frontend
seed.py            Populates initial currencies, balances, and rates
sync_rates.py      update fx rates daily from frankruter 


API endpoints

Currencies: /api/v1/currencies/
Stock: /api/v1/stock/
Exchange rates: /api/v1/rates/
Transactions: /api/v1/transactions/
Dashboard: /api/v1/dashboard/
AI assistant: /api/v1/ai/query

Full interactive documentation is available at /docs once the server is running
