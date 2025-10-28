# Development Guide

This guide will help you set up the development environment and run the FastAPI server with PostgreSQL database connection.

## Prerequisites

Before starting, ensure you have the following installed:

- **Python 3.13+** - [Download](https://www.python.org/downloads/)
- **PostgreSQL 18** - [Download](https://www.postgresql.org/download/)
- **Git** - [Download](https://git-scm.com/downloads)

## Initial Setup

### 1. Clone the Repository

```bash
git clone https://github.com/jd-velop/guess-street-main.git
cd guess-street-main
```

### 2. Set Up Python Virtual Environment

Navigate to the backend directory and create a virtual environment:

```bash
cd backend
python -m venv venv
```

Activate the virtual environment:

**Windows (PowerShell):**
```powershell
.\venv\Scripts\Activate.ps1
```

**Windows (Command Prompt):**
```cmd
.\venv\Scripts\activate.bat
```

### 3. Install Python Dependencies

With the virtual environment activated, install all required packages:

```bash
pip install -r requirements.txt
```

This will install:
- FastAPI - Web framework
- Uvicorn - ASGI server
- SQLAlchemy - ORM for database operations
- psycopg2-binary - PostgreSQL adapter
- python-dotenv - Environment variable management
- pydantic-settings - Settings management
- APScheduler - Task scheduling

## Database Setup

### 1. Install and Start PostgreSQL

Make sure PostgreSQL is installed and running:

**Windows:**
- Open Services (Win + R, type `services.msc`)
- Find "postgresql-x64-18" service
- Ensure it's running (right-click → Start if not)


### 2. Configure Database Connection

Create a `.env` file in the `backend` directory:

```bash
# backend/.env
DATABASE_URL=postgresql://postgres:YOUR_PASSWORD@localhost:5432/guess_street
```

**Important Notes:**
- Replace `YOUR_PASSWORD` with your actual PostgreSQL password
- If your password contains special characters, they must be URL-encoded:
  - `@` → `%40`
  - `!` → `%21`
  - `#` → `%23`
  - `$` → `%24`
  - `%` → `%25`
  - `^` → `%5E`
  - `&` → `%26`
  - `*` → `%2A`

**Example:**
```bash
# If your password is: MyP@ss!2024
# URL-encoded version is: MyP%40ss%212024
DATABASE_URL=postgresql://postgres:MyP%40ss%212024@localhost:5432/guess_street
```

### 3. Create the Database

You can create the database using one of two methods:

#### Option A: Using pgAdmin (GUI)
1. Open pgAdmin
2. Connect to your PostgreSQL server
3. Right-click on "Databases" → "Create" → "Database"
4. Name it `guess_street`
5. Click "Save"

#### Option B: Using psql (Command Line)
```bash
psql -U postgres
CREATE DATABASE guess_street;
\q
```
### 4. Initialize Database Tables

The FastAPI application will automatically create the required tables on startup. The tables include:
- `predictions` - Stores asset predictions with min/max values and target dates

## Running the Development Server

### 1. Start the FastAPI Server

With your virtual environment activated and database configured:

```bash
# From the backend directory
uvicorn main:app --reload
```

The `--reload` flag enables auto-reload when you make code changes.

### 2. Verify Server is Running

You should see output like:
```
INFO:     Uvicorn running on http://127.0.0.1:8000 (Press CTRL+C to quit)
INFO:     Started reloader process [12345] using WatchFiles
INFO:     Started server process [67890]
INFO:     Waiting for application startup.
✅ Database tables initialized
INFO:     Application startup complete.
```

### 3. Access API Documentation

FastAPI provides automatic interactive API documentation:

- **Swagger UI:** http://127.0.0.1:8000/docs
- **ReDoc:** http://127.0.0.1:8000/redoc

![API Homepage](Assets/API_Homepage.png)
*FastAPI interactive documentation homepage showing all available endpoints*

## Testing the API

### Using the Browser (Swagger UI)

1. Go to http://127.0.0.1:8000/docs
2. Click on any endpoint (e.g., "POST /predictions")
3. Click "Try it out"

   ![Default POST Prediction Form](Assets/Post_Prediction_Default.png)
   *Click "Try it out" to enable the form*

4. Fill in the request body

   ![Filled Out POST Prediction Form](Assets/Post_Prediction_Filled_Out.png)
   *Example prediction request with all fields filled*

5. Click "Execute"

   ![POST Prediction Response](Assets/Post_Prediction_Responses.png)
   *Successful response showing the created prediction with server-generated ID and timestamp*



### Using cURL

**Create a Prediction:**
```bash
curl -X POST "http://127.0.0.1:8000/predictions" \
  -H "Content-Type: application/json" \
  -d '{
    "asset": "BTC",
    "predictor": "john_doe",
    "min_value": 50000,
    "max_value": 55000,
    "target_date": "2025-12-31"
  }'
```

**Get All Predictions:**
```bash
curl -X GET "http://127.0.0.1:8000/predictions"
```

**Get a Specific Prediction:**
```bash
curl -X GET "http://127.0.0.1:8000/predictions/{prediction_id}"
```

## Project Structure

```
guess-street-main/
├── backend/
│   ├── venv/                 # Virtual environment (not in git)
│   ├── .env                  # Environment variables (not in git)
│   ├── main.py               # FastAPI application entry point
│   ├── database.py           # Database configuration and models
│   ├── prediction.py         # Pydantic models for API validation
│   ├── auth.py               # Authentication logic (future)
│   ├── scheduler.py          # Task scheduling (future)
│   ├── requirements.txt      # Python dependencies
│   └── setup_database.py     # Database initialization script
├── .gitignore                # Git ignore rules
└── README.md                 # Project overview
```

## Common Issues and Solutions

### Issue: "ModuleNotFoundError"
**Solution:** Make sure your virtual environment is activated and dependencies are installed:
```bash
pip install -r requirements.txt
```

### Issue: "connection to server failed"
**Solution:** 
- Verify PostgreSQL service is running
- Check that the DATABASE_URL in `.env` is correct
- Verify the database `guess_street` exists

### Issue: "password authentication failed"
**Solution:**
- Double-check your PostgreSQL password
- Ensure special characters are URL-encoded in `.env`
- Try connecting with psql to verify credentials work:
  ```bash
  psql -U postgres -d guess_street
  ```

### Issue: "could not connect to server: Connection refused"
**Solution:**
- Check if PostgreSQL is running on port 5432
- Verify PostgreSQL service is started
- Check firewall settings aren't blocking port 5432

### Issue: Virtual environment activation fails
**Solution (Windows PowerShell):**
If you see an execution policy error, run:
```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

## Environment Variables Reference

| Variable | Description | Example |
|----------|-------------|---------|
| `DATABASE_URL` | PostgreSQL connection string | `postgresql://postgres:password@localhost:5432/guess_street` |

## Development Workflow

1. **Activate virtual environment** before working on the project
2. **Start PostgreSQL** service if not already running
3. **Run the server** with `uvicorn main:app --reload`
4. **Make code changes** - server will auto-reload
5. **Test changes** using http://127.0.0.1:8000/docs
6. **Deactivate virtual environment** when done: `deactivate`

## Stopping the Server

Press `CTRL + C` in the terminal where uvicorn is running.

## Database Management

### View Database Tables

Using psql:
```bash
psql -U postgres -d guess_street
\dt              # List all tables
\d predictions   # Describe predictions table
SELECT * FROM predictions;  # View all predictions
\q               # Quit
```

### Reset Database

To start fresh:
```sql
DROP TABLE predictions;
```

Then restart the FastAPI server to recreate tables.

## Additional Resources

- [FastAPI Documentation](https://fastapi.tiangolo.com/)
- [SQLAlchemy Documentation](https://docs.sqlalchemy.org/)
- [PostgreSQL Documentation](https://www.postgresql.org/docs/)
- [Uvicorn Documentation](https://www.uvicorn.org/)
# Development
