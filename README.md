# Tex2SQL - AI-Powered Text-to-SQL Platform

[![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)](https://python.org)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.104+-green.svg)](https://fastapi.tiangolo.com)
[![React](https://img.shields.io/badge/React-18+-blue.svg)](https://reactjs.org)
[![TypeScript](https://img.shields.io/badge/TypeScript-5+-blue.svg)](https://typescriptlang.org)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-13+-blue.svg)](https://postgresql.org)

An intelligent text-to-SQL platform that converts natural language questions into SQL queries using AI. Built with FastAPI backend, React frontend, and powered by Vanna.AI with OpenAI integration for Microsoft SQL Server databases.

## 🚀 Features

### Core Functionality
- **Natural Language to SQL**: Convert plain English questions into SQL queries
- **Multi-User Support**: User authentication and personalized workspaces
- **Database Connections**: Connect to Microsoft SQL Server databases with full management
- **AI Training**: Train custom AI models on your specific database schema and data
- **Real-time Chat Interface**: Interactive conversation-based querying
- **Data Visualization**: Automatic chart generation using Plotly
- **Query Results**: Execute generated SQL and display formatted results

### Advanced Features
- **Schema Analysis**: Automatic database schema detection and analysis
- **Column Descriptions**: AI-generated or manual column documentation
- **Training Data Management**: Generate and manage question-SQL training pairs
- **Real-time Streaming**: Server-Sent Events (SSE) for live progress updates
- **Connection Management**: Test, configure, and manage multiple database connections
- **Conversation History**: Persistent chat history with full conversation management

### Security & Performance
- **JWT Authentication**: Secure user authentication with access/refresh tokens
- **Password Security**: Strong password requirements and validation
- **Connection Encryption**: Secure database connections with encryption support
- **Input Validation**: Comprehensive request validation and sanitization
- **Error Handling**: Robust error handling with detailed logging

## 🏗️ Architecture

### Backend (FastAPI)
```
backend/
├── app/
│   ├── api/           # API endpoints
│   ├── core/          # Core functionality (database, SSE, Vanna wrapper)
│   ├── models/        # Data models and schemas
│   ├── services/      # Business logic
│   ├── utils/         # Utilities and helpers
│   └── main.py        # FastAPI application
├── alembic/           # Database migrations
├── scripts/           # Utility scripts
└── client/            # Python client example
```

### Frontend (React + TypeScript)
```
frontend/
├── src/
│   ├── components/    # React components
│   │   ├── auth/      # Authentication components
│   │   ├── chat/      # Chat interface
│   │   ├── connection/ # Database connection management
│   │   └── ui/        # Reusable UI components
│   ├── contexts/      # React contexts
│   ├── hooks/         # Custom React hooks
│   ├── pages/         # Main pages
│   ├── services/      # API services
│   ├── types/         # TypeScript types
│   └── utils/         # Utilities
└── public/            # Static assets
```

### Key Technologies
- **Backend**: FastAPI, SQLAlchemy, Asyncpg, Alembic, Vanna.AI
- **Frontend**: React 18, TypeScript, Tailwind CSS, Lucide Icons
- **Database**: PostgreSQL (application), Microsoft SQL Server (target)
- **AI/ML**: OpenAI GPT-4, Vanna.AI, ChromaDB (vector storage)
- **Real-time**: Server-Sent Events (SSE)
- **Visualization**: Plotly.js, React-Plotly
- **Authentication**: JWT tokens with refresh mechanism

## 📋 Prerequisites

- **Python 3.8+** with pip
- **Node.js 16+** with npm
- **PostgreSQL 13+** (for application database)
- **Microsoft SQL Server** (target database for queries)
- **OpenAI API Key** (GPT-4 access required)

## 🚀 Quick Start

### 1. Clone the Repository
```bash
git clone <repository-url>
cd tex2sql
```

### 2. Environment Configuration

Create a `.env` file in the `backend/` directory:

```env
# Database Configuration
DATABASE_URL=postgresql+asyncpg://postgres:password@localhost:5432/tex2sql

# OpenAI Configuration (Required)
OPENAI_API_KEY=your_openai_api_key_here
OPENAI_BASE_URL=https://api.openai.com/v1
OPENAI_MODEL=gpt-4

# Security
SECRET_KEY=your_secret_key_here
ALGORITHM=HS256
ACCESS_TOKEN_EXPIRE_MINUTES=30

# Application Settings
DEBUG=true
APP_NAME=Tex2SQL API
```

### 3. Backend Setup

```bash
cd backend

# Create virtual environment
python -m venv .venv
source .venv/bin/activate  # On Windows: .venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Run database migrations
alembic upgrade head

# Verify setup
python scripts/verify_setup.py

# Start the API server
python scripts/run_api.sh
# Or manually: uvicorn app.main:app --port 6020 --reload
```

The backend will be available at: `http://localhost:6020`

### 4. Frontend Setup

```bash
cd frontend

# Install dependencies
npm install

# Start development server
npm start
```

The frontend will be available at: `http://localhost:3000`

### 5. Database Setup

Ensure PostgreSQL is running and create the database:

```sql
CREATE DATABASE tex2sql;
CREATE USER tex2sql_user WITH PASSWORD 'your_password';
GRANT ALL PRIVILEGES ON DATABASE tex2sql TO tex2sql_user;
```

## 📖 Usage Guide

### 1. User Registration & Login

1. Navigate to `http://localhost:3000`
2. Register a new account or login with existing credentials

### 2. Database Connection Setup

1. Go to **Connections** page
2. Click **Add New Connection**
3. Configure your Microsoft SQL Server connection:
   - Server address
   - Database name
   - Username/password
   - Table name (schema.table format)
   - Encryption settings

### 3. Connection Testing & Training

1. **Test Connection**: Verify database connectivity
2. **Generate Column Descriptions**: Use AI to analyze schema
3. **Generate Training Data**: Create question-SQL examples (optional)
4. **Train Model**: Train the AI model on your database

### 4. Querying with Natural Language

1. Navigate to the **Chat** interface
2. Select a trained connection
3. Ask questions in natural language:
   - "Show me the top 10 customers by sales"
   - "What's the average order value last month?"
   - "Find all products with low inventory"

### 5. Managing Conversations

- **New Conversation**: Start fresh conversations
- **Conversation History**: Access previous conversations
- **Connection Switching**: Change database connections mid-conversation

## 🔧 Configuration

### Backend Configuration

Key settings in `backend/app/config.py`:

```python
# Authentication
ACCESS_TOKEN_EXPIRE_MINUTES = 30
PASSWORD_MIN_LENGTH = 8
MAX_SESSIONS_PER_USER = 5

# File Upload
MAX_UPLOAD_SIZE = 10 * 1024 * 1024  # 10MB
ALLOWED_FILE_TYPES = [".csv", ".xlsx", ".json"]

# Query Settings
MAX_QUERY_EXECUTION_TIME = 300  # 5 minutes
MAX_RESULT_ROWS = 10000

# SSE Configuration
SSE_HEARTBEAT_INTERVAL = 30
SSE_CONNECTION_TIMEOUT = 300
```

### Frontend Configuration

Modify `frontend/src/services/` for API endpoints and configurations.

## 🛠️ Development

### Backend Development

```bash
cd backend

# Install development dependencies
pip install -r requirements-dev.txt

# Run tests
python -m pytest

# Database reset (development only)
bash scripts/reset_db.sh

# Generate new migration
alembic revision --autogenerate -m "description"
```

### Frontend Development

```bash
cd frontend

# Run with mock server
npm run dev

# Build for production
npm run build

# Run tests
npm test
```

### API Documentation

Once the backend is running, visit:
- **Swagger UI**: `http://localhost:6020/docs`
- **ReDoc**: `http://localhost:6020/redoc`

## 🐳 Docker Deployment

### Development
```bash
# Build images
docker compose build

# Start services
docker compose up -d
```

### Production
```bash
# Build and push to registry
./push.sh

# Deploy with production configuration
docker compose -f docker-compose.prod.yml up -d
```

## 📚 API Reference

### Authentication Endpoints
- `POST /auth/register` - User registration
- `POST /auth/login` - User login
- `POST /auth/refresh` - Token refresh

### Connection Management
- `GET /connections/` - List connections
- `POST /connections/` - Create connection
- `PUT /connections/{id}` - Update connection
- `DELETE /connections/{id}` - Delete connection
- `POST /connections/test` - Test connection

### Training & AI
- `POST /training/generate-data/{connection_id}` - Generate training data
- `POST /training/train/{connection_id}` - Train AI model
- `GET /training/data/{connection_id}` - Get training data

### Conversations & Queries
- `GET /conversations/` - List conversations
- `POST /conversations/` - Create conversation
- `POST /conversations/query` - Query with natural language
- `GET /events/stream/{session_id}` - SSE stream for real-time updates

## 🧪 Testing

### Python Client Example

```python
import asyncio
from backend.client.tex2sql_client import Tex2SQLClient

async def example_usage():
    async with Tex2SQLClient("http://localhost:6020") as client:
        # Authenticate
        await client.authenticate_user("username", "email@example.com", "password")
        
        # Create connection
        connection_data = {
            "name": "My Database",
            "server": "localhost",
            "database_name": "mydb",
            "username": "user",
            "password": "pass",
            "table_name": "schema.table"
        }
        
        connection = await client.create_connection(connection_data)
        
        # Train model
        await client.train_model(connection["id"])
        
        # Query
        conversation = await client.create_conversation(connection["id"])
        await client.query_database(conversation["id"], "Show me the top 10 records")

asyncio.run(example_usage())
```

## 🔍 Troubleshooting

### Common Issues

**Database Connection Failed**
- Verify PostgreSQL is running
- Check DATABASE_URL in .env file
- Ensure database exists and user has permissions

**OpenAI API Errors**
- Verify OPENAI_API_KEY is set correctly
- Check API key has GPT-4 access
- Ensure sufficient API credits

**Training Fails**
- Check database connection is tested successfully
- Verify sufficient training data exists
- Check ChromaDB permissions in data/ directory

**Frontend Connection Issues**
- Ensure backend is running on port 6020
- Check CORS configuration
- Verify API endpoints in frontend services

### Logs and Debugging

**Backend Logs**
```bash
# View application logs
tail -f logs/tex2sql.log

# Database query logs
export SQLALCHEMY_ECHO=true
```

**Frontend Debugging**
- Open browser developer tools
- Check Network tab for API calls
- Monitor Console for JavaScript errors


## 🙏 Acknowledgments

- **Vanna.AI** - Text-to-SQL AI framework
- **OpenAI** - GPT-4 language model
- **FastAPI** - Modern Python web framework
- **React** - Frontend framework
- **PostgreSQL** - Database system

