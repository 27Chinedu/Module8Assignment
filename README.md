# FastAPI Calculator - RESTful API Learning Guide

**A comprehensive beginner-friendly project for learning RESTful APIs, testing, and containerization using FastAPI.**

## What is a RESTful API?

> **REST** (Representational State Transfer) is an architectural style for designing networked applications. A **RESTful API** is a web service that follows REST principles.

### Core Principles

| Principle | Description |
|-----------|-------------|
| **Client-Server Architecture** | The client (browser/app) and server are separate |
| **Stateless** | Each request contains all information needed; the server doesn't store client state |
| **Resource-Based** | Everything is a "resource" (like `/add`, `/subtract`) |
| **HTTP Methods** | Uses standard HTTP methods (GET, POST, PUT, DELETE) |
| **JSON Format** | Data is typically exchanged in JSON format |

### In This Project

- **Resources**: Calculator operations (`/add`, `/subtract`, `/multiply`, `/divide`)
- **HTTP Method**: POST (we send data to the server)
- **Request Format**: JSON with two numbers: `{"a": 10, "b": 5}`
- **Response Format**: JSON with result: `{"result": 15}` or error: `{"error": "message"}`


## Project Overview

This project is a **calculator application** that demonstrates RESTful API concepts through a simple, interactive web interface.

| Component | Technology |
|-----------|-----------|
| 🎨 **Frontend** | HTML, CSS, JavaScript |
| ⚙️ **Backend** | FastAPI (Python) |
| 🧮 **Operations** | Add, Subtract, Multiply, Divide |
| 🧪 **Testing** | Unit, Integration, E2E (Pytest, Playwright) |
| 🐳 **Deployment** | Docker, Docker Compose, CI/CD |

</div>

### What I Learned

<table>
  <tr>
    <td> Building RESTful APIs with FastAPI</td>
    <td> Request/response handling</td>
  </tr>
  <tr>
    <td> Error handling and validation</td>
    <td> Writing comprehensive tests</td>
  </tr>
  <tr>
    <td> Docker containerization</td>
    <td> CI/CD with GitHub Actions</td>
  </tr>
  <tr>
    <td> Security best practices</td>
    <td> API documentation (Swagger/ReDoc)</td>
  </tr>
</table>  

### Request Flow:

1. User enters numbers in the browser
2. JavaScript sends POST request to API endpoint
3. FastAPI receives and validates the request
4. Operation function performs calculation
5. FastAPI returns JSON response
6. JavaScript displays result to user


## Prerequisites

Before starting, ensure you have:

- **Python 3.10+** installed
- **Git** installed and configured
- **Docker Desktop** (optional, for containerization)
- A **text editor** (VS Code recommended)
- Basic knowledge of **Python** and **command line**

### Check Installations:

```bash
python --version    # Should show Python 3.10 or higher
git --version       # Should show Git version
docker --version    # Should show Docker version (if installed)
```


## Understanding the API

### API Endpoints

| Endpoint | Method | Description | Example Request | Example Response |
|----------|--------|-------------|-----------------|------------------|
| `/` | GET | Serves homepage | - | HTML page |
| `/add` | POST | Adds two numbers | `{"a": 10, "b": 5}` | `{"result": 15}` |
| `/subtract` | POST | Subtracts b from a | `{"a": 10, "b": 5}` | `{"result": 5}` |
| `/multiply` | POST | Multiplies two numbers | `{"a": 10, "b": 5}` | `{"result": 50}` |
| `/divide` | POST | Divides a by b | `{"a": 10, "b": 2}` | `{"result": 5.0}` |

### Testing Endpoints with cURL

**Addition:**
```bash
curl -X POST "http://localhost:8000/add" \
  -H "Content-Type: application/json" \
  -d '{"a": 10, "b": 5}'
```

**Division by Zero (Error Handling):**
```bash
curl -X POST "http://localhost:8000/divide" \
  -H "Content-Type: application/json" \
  -d '{"a": 10, "b": 0}'
```

**Expected Error Response:**
```json
{
  "error": "Cannot divide by zero!"
}
```

### Interactive API Documentation

FastAPI automatically generates interactive documentation:

- **Swagger UI**: http://localhost:8000/docs
- **ReDoc**: http://localhost:8000/redoc


###  Why Use Docker?

| Benefit | Description |
|---------|-------------|
| **Consistency** | Works the same on all machines |
| **Isolation** | Dependencies don't conflict with your system |
| **Portability** | Easy to deploy anywhere |
| **Scalability** | Can run multiple containers |  



##  Project Structure

```
fastapi-calculator/
├── app/
│   └── operations/
│       └── __init__.py          # Calculator functions (add, subtract, etc.)
├── templates/
│   └── index.html               # Frontend HTML interface
├── tests/
│   ├── unit/
│   │   └── test_calculator.py   # Unit tests for operations
│   ├── integration/
│   │   └── test_fastapi_calculator.py  # API endpoint tests
│   └── e2e/
│       └── test_e2e.py          # Browser-based tests
├── .github/
│   └── workflows/
│       └── test.yml             # CI/CD pipeline configuration
├── main.py                      # FastAPI application entry point
├── Dockerfile                   # Docker image instructions
├── docker-compose.yml           # Docker Compose configuration
├── requirements.txt             # Python dependencies
├── pytest.ini                   # Pytest configuration
└── README.md                    # This file
```

---

## Key Concepts

### 1. FastAPI Framework

FastAPI is a modern Python web framework with:
- **Fast**: High performance (on par with NodeJS)
- **Type Hints**: Uses Python type hints for validation
- **Auto Documentation**: Generates Swagger/ReDoc automatically
- **Async Support**: Handles concurrent requests efficiently

### 2. Pydantic Models

Define data structure and validation:

```python
class OperationRequest(BaseModel):
    a: float = Field(..., description="The first number")
    b: float = Field(..., description="The second number")
```

This ensures:
- Only numbers are accepted
- Both fields are required
- Automatic validation errors if data is invalid

### 3. HTTP Status Codes

- **200 OK**: Request succeeded
- **400 Bad Request**: Invalid input (e.g., division by zero)
- **500 Internal Server Error**: Server-side error

### 4. JSON (JavaScript Object Notation)

A lightweight data format:

```json
{
  "a": 10,
  "b": 5
}
```

Easy for both humans and machines to read/write.
