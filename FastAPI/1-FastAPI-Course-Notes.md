# The Definitive FastAPI Course Notes: From Zero to Production

A comprehensive, hands-on, and production-grade master guide to building modern, robust, asynchronous APIs in Python using **FastAPI**.

---

## Table of Contents

### [Module 1: Introduction, Architecture & First Steps](#module-1-introduction-architecture--first-steps)
- [Chapter 1: Introduction to APIs, HTTP Methods, and REST Architecture](#chapter-1-introduction-to-apis-http-methods-and-rest-architecture)
  - [What is an API? The Restaurant Waiter Analogy](#what-is-an-api-the-restaurant-waiter-analogy)
  - [HTTP Fundamentals & Anatomy of Requests/Responses](#http-fundamentals--anatomy-of-requestsresponses)
  - [HTTP Methods & Semantic Purpose](#http-methods--semantic-purpose)
  - [HTTP Status Code Families](#http-status-code-families)
  - [Core REST Architectural Principles](#core-rest-architectural-principles)
- [Chapter 2: Python Development Environment, Virtual Environments, and Uvicorn/ASGI](#chapter-2-python-development-environment-virtual-environments-and-uvicornasgi)
  - [Why FastAPI? The Tech Stack Breakdown](#why-fastapi-the-tech-stack-breakdown)
  - [WSGI vs ASGI: The Concurrency Revolution](#wsgi-vs-asgi-the-concurrency-revolution)
  - [Setting Up a Virtual Environment & Installing FastAPI](#setting-up-a-virtual-environment--installing-fastapi)
  - [Project Folder Structures: Beginner vs Professional Layout](#project-folder-structures-beginner-vs-professional-layout)
- [Chapter 3: First Steps: Building Your First Application & Automatic Docs](#chapter-3-first-steps-building-your-first-application--automatic-docs)
  - [The Simplest Working FastAPI Application (Line-by-Line Breakdown)](#the-simplest-working-fastapi-application-line-by-line-breakdown)
  - [Running the Server with Uvicorn (Options & Flags)](#running-the-server-with-uvicorn-options--flags)
  - [Multiple Endpoints Example & Console Output Walkthrough](#multiple-endpoints-example--console-output-walkthrough)
  - [Interactive Documentation: Swagger UI, ReDoc, and OpenAPI](#interactive-documentation-swagger-ui-redoc-and-openapi)
- [Chapter 4: Path Operation Configuration, Metadata, Docs URLs & Static Files](#chapter-4-path-operation-configuration-metadata-docs-urls--static-files)
  - [Configuring Tags, Summary, Description, and Deprecation](#configuring-tags-summary-description-and-deprecation)
  - [Customizing API Metadata, OpenAPI URL, and Disabling Docs](#customizing-api-metadata-openapi-url-and-disabling-docs)
  - [Serving Static Files with StaticFiles](#serving-static-files-with-staticfiles)
  - [Folder Layout for Static Assets](#folder-layout-for-static-assets)

### [Module 2: Parameters, Validation & Advanced Request Data](#module-2-parameters-validation--advanced-request-data)
- [Chapter 5: Path Parameters and Numeric Validations](#chapter-5-path-parameters-and-numeric-validations)
  - [Dynamic Path Routing & Type Hints](#dynamic-path-routing--type-hints)
  - [Enum Path Parameters (Strict Choice Validation)](#enum-path-parameters-strict-choice-validation)
  - [Numeric Validation with Path (ge, le, gt, lt)](#numeric-validation-with-path-ge-le-gt-lt)
  - [Path Parameter Order Matters](#path-parameter-order-matters)
  - [Detailed Validation Error Outputs](#detailed-validation-error-outputs)
- [Chapter 6: Query Parameters and String Validations](#chapter-6-query-parameters-and-string-validations)
  - [Query Parameters with Defaults and Optional Values](#query-parameters-with-defaults-and-optional-values)
  - [String Validations with Query (Length & Regex Patterns)](#string-validations-with-query-length--regex-patterns)
  - [Receiving Lists / Multiple Values in Query Parameters](#receiving-lists--multiple-values-in-query-parameters)
  - [Advanced Real-World Filtering Example (E-Commerce Catalog)](#advanced-real-world-filtering-example-e-commerce-catalog)
- [Chapter 7: Request Body, Pydantic Models & Field Validations](#chapter-7-request-body-pydantic-models--field-validations)
  - [What is Pydantic? Parsing vs Validation](#what-is-pydantic-parsing-vs-validation)
  - [Creating Schemas with BaseModel & Field](#creating-schemas-with-basemodel--field)
  - [Pydantic V2 Custom Validators with @field_validator](#pydantic-v2-custom-validators-with-field_validator)
  - [Complete User Registration Schema Example](#complete-user-registration-schema-example)
- [Chapter 8: Body - Multiple Parameters, Singular Values & Embedding](#chapter-8-body---multiple-parameters-singular-values--embedding)
  - [Mixing Path, Query, and Body Parameters](#mixing-path-query-and-body-parameters)
  - [Multiple Pydantic Body Parameters](#multiple-pydantic-body-parameters)
  - [Singular Values in Body with Body(...)](#singular-values-in-body-with-body)
  - [Embed a Single Body Parameter with embed=True](#embed-a-single-body-parameter-with-embedtrue)
- [Chapter 9: Body - Nested Models, Deep Structures & Sets](#chapter-9-body---nested-models-deep-structures--sets)
  - [Nested Sub-Models](#nested-sub-models)
  - [Attributes with Lists and Sets for Uniqueness](#attributes-with-lists-and-sets-for-uniqueness)
  - [Deeply Nested Models and Dictionaries with Arbitrary Keys](#deeply-nested-models-and-dictionaries-with-arbitrary-keys)
  - [Complete Order & Line-Item Invoice Example](#complete-order--line-item-invoice-example)
- [Chapter 10: Extra Data Types](#chapter-10-extra-data-types)
  - [UUID, datetime, date, and timedelta](#uuid-datetime-date-and-timedelta)
  - [Decimal for Financial Accuracy](#decimal-for-financial-accuracy)
  - [Raw bytes Payloads](#raw-bytes-payloads)
  - [Complete SaaS Subscription Billing Model Example](#complete-saas-subscription-billing-model-example)
- [Chapter 11: Cookie & Header Parameters (Individual & Pydantic Models)](#chapter-11-cookie--header-parameters-individual--pydantic-models)
  - [Reading Cookies with Cookie(...)](#reading-cookies-with-cookie)
  - [Reading Headers with Header(...)](#reading-headers-with-header)
  - [Query Parameter Models](#query-parameter-models)
  - [Cookie Parameter Models & Header Parameter Models](#cookie-parameter-models--header-parameter-models)
- [Chapter 12: Request Forms, File Uploads, Form Models & Combined Requests](#chapter-12-request-forms-file-uploads-form-models--combined-requests)
  - [Form Data with Form(...)](#form-data-with-form)
  - [File Uploads: bytes vs UploadFile](#file-uploads-bytes-vs-uploadfile)
  - [Combining Form Fields and Uploaded Files in One Request](#combining-form-fields-and-uploaded-files-in-one-request)
  - [Uploading Multiple Files Simultaneously (List[UploadFile])](#uploading-multiple-files-simultaneously-listuploadfile)
  - [Request Form Models (Pydantic Models as Forms)](#request-form-models-pydantic-models-as-forms)

### [Module 3: Response Modeling, Error Handling & Data Transformation](#module-3-response-modeling-error-handling--data-transformation)
- [Chapter 13: Response Status Codes & Path Configuration](#chapter-13-response-status-codes--path-configuration)
  - [Explicit HTTP Status Codes with fastapi.status](#explicit-http-status-codes-with-fastapistatus)
  - [Setting Status Codes Dynamically with Response](#setting-status-codes-dynamically-with-response)
- [Chapter 14: Response Models & Return Type Annotations](#chapter-14-response-models--return-type-annotations)
  - [Data Filtering & Security: Why Response Models are Mandatory](#data-filtering--security-why-response-models-are-mandatory)
  - [Return Type vs response_model](#return-type-vs-response_model)
  - [Filtering Out Unset Data with response_model_exclude_unset](#filtering-out-unset-data-with-response_model_exclude_unset)
- [Chapter 15: Extra Models & Inheritance Patterns](#chapter-15-extra-models--inheritance-patterns)
  - [Model Inheritance: Base, Create, InDB, and Public Response](#model-inheritance-base-create-indb-and-public-response)
  - [Union Types for Polymorphic Response Models](#union-types-for-polymorphic-response-models)
  - [Schema Extra & OpenAPI Documentation Examples](#schema-extra--openapi-documentation-examples)
- [Chapter 16: Handling Errors & Custom Exception Handlers](#chapter-16-handling-errors--custom-exception-handlers)
  - [Raising HTTPException with Headers and Structured Details](#raising-httpexception-with-headers-and-structured-details)
  - [Custom Domain Exceptions & Global Handlers with @app.exception_handler](#custom-domain-exceptions--global-handlers-with-appexception_handler)
  - [Overriding Default Validation Error Handlers](#overriding-default-validation-error-handlers)
- [Chapter 17: JSON Compatible Encoder & Data Updates (PUT vs PATCH)](#chapter-17-json-compatible-encoder--data-updates-put-vs-patch)
  - [The Magic of jsonable_encoder](#the-magic-of-jsonable_encoder)
  - [Full Replacement with PUT vs Partial Update with PATCH](#full-replacement-with-put-vs-partial-update-with-patch)
  - [Using model_dump(exclude_unset=True) for Patching](#using-model_dumpexclude_unsettrue-for-patching)

### [Module 4: Dependency Injection, Middleware & Bigger Applications](#module-4-dependency-injection-middleware--bigger-applications)
- [Chapter 18: Dependency Injection Fundamentals](#chapter-18-dependency-injection-fundamentals)
  - [The Mental Model of Dependency Injection (The Hollywood Principle)](#the-mental-model-of-dependency-injection-the-hollywood-principle)
  - [Function Dependencies with Depends(...)](#function-dependencies-with-depends)
  - [Classes as Dependencies (Object-Oriented Injection)](#classes-as-dependencies-object-oriented-injection)
  - [Sub-dependencies: Resolving Hierarchical Dependency Graphs](#sub-dependencies-resolving-hierarchical-dependency-graphs)
- [Chapter 19: Advanced Dependencies: Decorators, Global & Yield Lifecycles](#chapter-19-advanced-dependencies-decorators-global--yield-lifecycles)
  - [Dependencies in Path Operation Decorators](#dependencies-in-path-operation-decorators)
  - [Global Application Dependencies](#global-application-dependencies)
  - [Dependencies with yield (Setup & Teardown Context)](#dependencies-with-yield-setup--teardown-context)
- [Chapter 20: Middleware & CORS](#chapter-20-middleware--cors)
  - [The Middleware Onion Architecture](#the-middleware-onion-architecture)
  - [Custom Timing & Logging Middleware](#custom-timing--logging-middleware)
  - [CORS (Cross-Origin Resource Sharing) Configuration](#cors-cross-origin-resource-sharing-configuration)
- [Chapter 21: Background Tasks](#chapter-21-background-tasks)
  - [Running Operations in the Background](#running-operations-in-the-background)
  - [Injecting BackgroundTasks into Endpoints & Dependencies](#injecting-backgroundtasks-into-endpoints--dependencies)
- [Chapter 22: Structuring Bigger Applications with APIRouter](#chapter-22-structuring-bigger-applications-with-apirouter)
  - [Why APIRouter is Essential for Real-World Codebases](#why-apirouter-is-essential-for-real-world-codebases)
  - [Modular Directory Structure: Complete File Walkthrough](#modular-directory-structure-complete-file-walkthrough)
  - [Prefixes, Tags, and Nested Sub-Routers](#prefixes-tags-and-nested-sub-routers)

### [Module 5: Databases & Data Management (SQLAlchemy & SQLModel)](#module-5-databases--data-management-sqlalchemy--sqlmodel)
- [Chapter 23: Introduction to Relational Databases (SQLite & PostgreSQL)](#chapter-23-introduction-to-relational-databases-sqlite--postgresql)
  - [Database Concepts for API Developers](#database-concepts-for-api-developers)
  - [SQLite vs PostgreSQL Comparison](#sqlite-vs-postgresql-comparison)
- [Chapter 24: Modern SQLAlchemy 2.0 Integration & Full CRUD](#chapter-24-modern-sqlalchemy-20-integration--full-crud)
  - [SQLAlchemy 2.0 Declarative Base, Mapped, and mapped_column](#sqlalchemy-20-declarative-base-mapped-and-mapped_column)
  - [Database Engine, SessionLocal, and get_db Dependency](#database-engine-sessionlocal-and-get_db-dependency)
  - [Full End-to-End CRUD Implementation (Create, Read, Update, Delete)](#full-end-to-end-crud-implementation-create-read-update-delete)
  - [One-to-Many Relationships (Authors & Books Example)](#one-to-many-relationships-authors--books-example)
- [Chapter 25: SQL Databases with SQLModel](#chapter-25-sql-databases-with-sqlmodel)
  - [What is SQLModel? Merging Pydantic and SQLAlchemy](#what-is-sqlmodel-merging-pydantic-and-sqlalchemy)
  - [Creating Table Models and Pydantic Schemas in One Class](#creating-table-models-and-pydantic-schemas-in-one-class)
  - [CRUD Operations with SQLModel and FastAPI](#crud-operations-with-sqlmodel-and-fastapi)
- [Chapter 26: Database Migrations using Alembic](#chapter-26-database-migrations-using-alembic)
  - [Why Database Migrations are Mandatory](#why-database-migrations-are-mandatory)
  - [Initializing Alembic & Configuring env.py](#initializing-alembic--configuring-envpy)
  - [Autogenerating, Upgrading, and Rolling Back Migrations](#autogenerating-upgrading-and-rolling-back-migrations)
  - [Folder Layout for Database Migrations](#folder-layout-for-database-migrations)

### [Module 6: Security, Testing & Production Deployment](#module-6-security-testing--production-deployment)
- [Chapter 27: Password Hashing (Bcrypt) & Security Fundamentals](#chapter-27-password-hashing-bcrypt--security-fundamentals)
  - [Why Plaintext Passwords Mean Catastrophe](#why-plaintext-passwords-mean-catastrophe)
  - [One-Way Cryptographic Hashing with Passlib & Bcrypt](#one-way-cryptographic-hashing-with-passlib--bcrypt)
- [Chapter 28: OAuth2, JWT Tokens, and User Authentication](#chapter-28-oauth2-jwt-tokens-and-user-authentication)
  - [OAuth2 Password Flow & JWT Token Anatomy](#oauth2-password-flow--jwt-token-anatomy)
  - [Issuing Signed JWT Access Tokens](#issuing-signed-jwt-access-tokens)
  - [The get_current_user Dependency Guard](#the-get_current_user-dependency-guard)
- [Chapter 29: Role-Based Access Control (RBAC) & Protected Routes](#chapter-29-role-based-access-control-rbac--protected-routes)
  - [Role Checking Dependency Factories](#role-checking-dependency-factories)
  - [Securing Admin and Privileged Endpoints](#securing-admin-and-privileged-endpoints)
- [Chapter 30: Asynchronous Programming in Python (async def vs def)](#chapter-30-asynchronous-programming-in-python-async-def-vs-def)
  - [How FastAPI Routes async def vs normal def](#how-fastapi-routes-async-def-vs-normal-def)
  - [The Danger of Blocking Synchronous Calls on the Event Loop](#the-danger-of-blocking-synchronous-calls-on-the-event-loop)
- [Chapter 31: Real-time Communication with WebSockets and Streaming](#chapter-31-real-time-communication-with-websockets-and-streaming)
  - [WebSockets vs HTTP Polling](#websockets-vs-http-polling)
  - [Multi-Client Broadcast WebSocket Manager](#multi-client-broadcast-websocket-manager)
  - [StreamingResponse & Server-Sent Events (SSE)](#streamingresponse--server-sent-events-sse)
- [Chapter 32: Automated Testing with pytest and TestClient](#chapter-32-automated-testing-with-pytest-and-testclient)
  - [FastAPI TestClient with httpx](#fastapi-testclient-with-httpx)
  - [In-Memory Test Database Fixtures & Dependency Overrides](#in-memory-test-database-fixtures--dependency-overrides)
  - [Writing Comprehensive Test Cases with Expected Assertions](#writing-comprehensive-test-cases-with-expected-assertions)
- [Chapter 33: Containerization with Docker & Production Deployment](#chapter-33-containerization-with-docker--production-deployment)
  - [Production Multi-Stage Dockerfile](#production-multi-stage-dockerfile)
  - [docker-compose.yml for FastAPI & PostgreSQL](#docker-composeyml-for-fastapi--postgresql)
  - [Nginx Reverse Proxy Configuration (nginx.conf)](#nginx-reverse-proxy-configuration-nginxconf)
  - [Production Architecture: Nginx + Gunicorn (Uvicorn Workers)](#production-architecture-nginx--gunicorn-uvicorn-workers)
- [Master Quick-Reference Summary](#master-quick-reference-summary)

---

# Module 1: Introduction, Architecture & First Steps

---

## Chapter 1: Introduction to APIs, HTTP Methods, and REST Architecture

### What is an API? The Restaurant Waiter Analogy

An **API** (Application Programming Interface) is a formal contract allowing two computer systems to communicate over a network.

Think of an API like a **waiter in a busy restaurant**:
- **The Customer (Client / Frontend):** You sit at a table looking at a printed menu (the API specification).
- **The Kitchen (Server / Database):** The kitchen prepares dishes, stores raw meats, and keeps secret recipes hidden away.
- **The Waiter (The API):** You tell the waiter: *"Bring me Pizza #3"*. The waiter carries your order to the kitchen, waits for the chefs to bake it, and returns the finished pizza to your table. You do not need to know the temperature of the oven, how the flour was kneaded, or where the chef bought the cheese.

```
+-------------------+             HTTP Request            +-------------------+
|                   |  -------------------------------->  |                   |
|  Client           |                                     |  Server           |
|  (React/iOS/cURL) |  <--------------------------------  |  (FastAPI Backend)|
|                   |             JSON Response           |                   |
+-------------------+                                     +-------------------+
                                                                    |
                                                          SQL Query |
                                                                    v
                                                          +-------------------+
                                                          |  Database         |
                                                          |  (PostgreSQL)     |
                                                          +-------------------+
```

> [!NOTE]
> **Author's Thought & Mental Model:** In modern software architecture, the backend server should almost never render HTML pages directly unless you are building a legacy monolith. Modern APIs return pure structured data (JSON). This gives you the superpower to support a Web dashboard, an iOS app, an Android app, and third-party developer integrations all from a single unified FastAPI backend!

### HTTP Fundamentals & Anatomy of Requests/Responses

Modern web APIs communicate over **HTTP** (Hypertext Transfer Protocol). An exchange consists of an incoming **Request** and a returned **Response**.

#### Anatomy of an HTTP Request
1. **Request Line:** Method + Path + Protocol Version (`POST /api/v1/orders HTTP/1.1`)
2. **Headers:** Key-value metadata (`Content-Type: application/json`, `Authorization: Bearer <token>`)
3. **Body (Payload):** Raw serialized data (typically JSON).

```http
POST /api/v1/orders HTTP/1.1
Host: api.devstore.com
User-Agent: Mozilla/5.0 (iPhone)
Content-Type: application/json
Authorization: Bearer eyJhbGciOiJIUzI1Ni...

{
  "product_id": 42,
  "quantity": 2
}
```

#### Anatomy of an HTTP Response
1. **Status Line:** Protocol + Status Code + Reason Phrase (`HTTP/1.1 201 Created`)
2. **Headers:** Key-value metadata (`Content-Type: application/json`, `Set-Cookie: ...`)
3. **Body:** The returned resource data or error message.

```http
HTTP/1.1 201 Created
Date: Tue, 27 Oct 2026 14:15:30 GMT
Content-Type: application/json
Content-Length: 78

{
  "order_id": 1092,
  "status": "confirmed",
  "total_usd": 59.98
}
```

### HTTP Methods & Semantic Purpose

| Method | CRUD Action | Idempotent? | Safe? | Description |
| :--- | :--- | :--- | :--- | :--- |
| **GET** | Read | Yes | Yes | Retrieve resource(s). Must never alter server state. |
| **POST** | Create | No | No | Submit data to create a new resource. |
| **PUT** | Full Replace | Yes | No | Completely replace an existing resource with a new representation. |
| **PATCH** | Partial Update | No | No | Update specific fields of an existing resource. |
| **DELETE** | Delete | Yes | No | Permanently remove a resource. |
| **OPTIONS** | Preflight | Yes | Yes | Inquire about permitted communication methods (used by CORS). |
| **HEAD** | Metadata | Yes | Yes | Identical to GET, but returns headers only without the body. |

> **Idempotent:** Calling the method 1 time produces the exact same server state as calling it 1,000 times (e.g., `DELETE /users/5`).

### HTTP Status Code Families

```
1xx (Informational) -> Request received, continuing process (e.g., 101 Switching Protocols)
2xx (Success)       -> Action successfully understood and accepted (e.g., 200 OK, 201 Created, 204 No Content)
3xx (Redirection)   -> Further action needed to complete request (e.g., 301 Moved Permanently, 304 Not Modified)
4xx (Client Error)  -> Request contains bad syntax or unauthorized parameters (e.g., 400 Bad Request, 401 Unauthorized, 403 Forbidden, 404 Not Found, 422 Unprocessable Entity)
5xx (Server Error)  -> Server failed to fulfill a valid request (e.g., 500 Internal Server Error, 502 Bad Gateway)
```

### Core REST Architectural Principles

1. **Client-Server Separation:** The client handles user interface concerns; the server handles storage and logic.
2. **Statelessness:** Every request contains all information needed to process it. The server never stores client session state across calls.
3. **Cacheability:** Responses explicitly declare whether they may be cached.
4. **Uniform Interface:** Resource identifiers must be clean, noun-based paths:
   - `GET /api/v1/courses` (List courses)
   - `POST /api/v1/courses` (Create course)
   - `GET /api/v1/courses/42` (Retrieve course 42)
   - `DELETE /api/v1/courses/42` (Delete course 42)
   - *Anti-pattern:* `GET /api/v1/getCourseById?id=42` or `POST /api/v1/deleteCourse/42`

---

## Chapter 2: Python Development Environment, Virtual Environments, and Uvicorn/ASGI

### Why FastAPI? The Tech Stack Breakdown

FastAPI delivers exceptional performance and developer ergonomics by combining two industry-standard libraries:

```
+-------------------------------------------------------------+
|                          FASTAPI                            |
|       (Dependency Injection, Auto Docs, Security, Routing)  |
+------------------------------+------------------------------+
|          STARLETTE           |           PYDANTIC           |
| (ASGI, WebSockets, Requests) | (Data Validation & Schemas)  |
+------------------------------+------------------------------+
```

1. **Starlette:** Handles the underlying ASGI web server, connection lifecycles, routing, HTTP exceptions, WebSockets, and background tasks.
2. **Pydantic (V2):** High-speed Rust-powered data parsing, type validation, and serialization.

### WSGI vs ASGI: The Concurrency Revolution

Traditional Python web frameworks like Flask and Django were built on **WSGI** (Web Server Gateway Interface). WSGI is **synchronous**: one worker process handles exactly one request at a time. If an endpoint takes 2 seconds to query a database, that worker is locked.

**ASGI** (Asynchronous Server Gateway Interface) allows a single Python process to handle thousands of concurrent connections using an **event loop**:

```
WSGI (Synchronous, 1 Thread per Request):
Worker 1: [--- Request 1 (Blocked on DB) --->][--- Request 2 --->]
Worker 2: [--- Request 3 (Blocked on DB) --->]

ASGI (Asynchronous Event Loop, Non-blocking Concurrency):
Loop: [Req 1 wait DB] -> [Req 2 wait DB] -> [Req 3 compute] -> [Req 1 DB ready -> finish]
```

### Setting Up a Virtual Environment & Installing FastAPI

Always isolate your project dependencies:

```bash
# 1. Create project directory
mkdir fastapi-mastery && cd fastapi-mastery

# 2. Create virtual environment
python3 -m venv .venv

# 3. Activate virtual environment
source .venv/bin/activate       # macOS / Linux
# .venv\Scripts\activate.bat    # Windows CMD
# .venv\Scripts\Activate.ps1    # Windows PowerShell

# 4. Install FastAPI with standard dependencies
pip install "fastapi[standard]"
```

Verify the installation:
```bash
python -c "import fastapi, uvicorn; print(fastapi.__version__, uvicorn.__version__)"
```

### Project Folder Structures: Beginner vs Professional Layout

#### 1. Beginner Single-File Project Layout
When starting out, prototyping an MVP, or writing quick microservices, a single-file or two-file structure is clean and easy to follow:

```text
fastapi-beginner/
├── .venv/                  # Isolated Python environment
├── main.py                 # All endpoints, Pydantic models, and app instance
├── requirements.txt        # Frozen dependencies (pip freeze > requirements.txt)
└── README.md               # Quick instructions on how to start the app
```

#### 2. Professional Production-Grade Layout
As your project grows to 10+ endpoints with database models, authentication, and external services, split concerns into dedicated packages:

```text
fastapi-production/
├── .venv/                      # Python virtual environment
├── app/
│   ├── __init__.py
│   ├── main.py                 # FastAPI app initialization, middleware, lifecycle
│   ├── core/                   # Application-wide configuration & security
│   │   ├── __init__.py
│   │   ├── config.py           # Pydantic BaseSettings (reads .env variables)
│   │   └── security.py         # Passlib password hashing & JWT token creators
│   ├── db/                     # Database engine & session lifecycles
│   │   ├── __init__.py
│   │   ├── database.py         # SQLAlchemy engine & SessionLocal
│   │   └── base.py             # DeclarativeBase metadata aggregator
│   ├── models/                 # SQLAlchemy Database Table Models
│   │   ├── __init__.py
│   │   ├── user.py             # User DB table
│   │   └── product.py          # Product DB table
│   ├── schemas/                # Pydantic Schemas (Request/Response contracts)
│   │   ├── __init__.py
│   │   ├── user.py             # UserCreate, UserUpdate, UserResponse
│   │   └── product.py          # ProductCreate, ProductResponse
│   ├── crud/                   # Database query logic (reusable functions)
│   │   ├── __init__.py
│   │   ├── crud_user.py
│   │   └── crud_product.py
│   └── routers/                # Modular API endpoints (APIRouter)
│       ├── __init__.py
│       ├── auth.py             # /token, /login
│       ├── users.py            # /users endpoints
│       └── products.py         # /products endpoints
├── tests/                      # Automated test suite (pytest)
│   ├── __init__.py
│   ├── conftest.py             # Test database fixtures & client overrides
│   ├── test_auth.py
│   └── test_products.py
├── static/                     # Static files (CSS, JS, images)
│   └── uploads/
├── .env                        # Local secret keys & database URLs (gitignored!)
├── .env.example                # Template of required environment variables
├── .gitignore
├── alembic.ini                 # Database migrations configuration
├── Dockerfile                  # Container packaging recipe
├── docker-compose.yml          # Multi-container orchestration (App + PostgreSQL)
└── requirements.txt
```

---

## Chapter 3: First Steps: Building Your First Application & Automatic Docs

### The Simplest Working FastAPI Application (Line-by-Line Breakdown)

Create a file named `main.py`:

```python
# main.py
from fastapi import FastAPI
from datetime import datetime

# Line 1: Create the application instance
app = FastAPI(
    title="DevStore Learning API",
    description="A comprehensive REST API for training and production reference",
    version="1.0.0"
)

# Line 2: The path operation decorator
@app.get("/")
def read_root():
    """
    Root health check endpoint.
    Returns a welcoming message along with current UTC timestamp.
    """
    # Line 3: Return a native Python dictionary
    return {
        "status": "online",
        "service": "DevStore Learning API",
        "timestamp": datetime.utcnow().isoformat()
    }
```

#### Step-by-Step Code Walkthrough:
1. `from fastapi import FastAPI`: Imports the core Python class that provides all API routing, validation, and documentation machinery.
2. `app = FastAPI(...)`: Instantiates the main application callable. This object is what Uvicorn will communicate with over the ASGI interface.
3. `@app.get("/")`:
   - `@app`: Refers to your FastAPI instance.
   - `.get(...)`: Specifies the HTTP method (**GET**). Other methods include `.post()`, `.put()`, `.patch()`, `.delete()`.
   - `"/"`: Specifies the URL path (the root route).
4. `def read_root():`: The Python function that runs whenever a client sends a `GET /` request.
5. `return {...}`: You can return Python `dict`, `list`, primitive values, or Pydantic models. FastAPI automatically serializes them into valid JSON!

### Running the Server with Uvicorn (Options & Flags)

In your terminal, execute:

```bash
uvicorn main:app --reload --port 8000
```

#### Useful Uvicorn Flags for Developers:
- `main:app`: Look in file `main.py` for the variable named `app`.
- `--reload`: Auto-reloads the server whenever any file in the workspace is saved. **Use only in development!**
- `--port 8000`: Binds the server to port 8000 (default is 8000).
- `--host 0.0.0.0`: Binds to all network interfaces. Required when running inside Docker containers or when testing from another device on your local Wi-Fi.
- `--workers 4`: Runs 4 parallel worker processes (mutually exclusive with `--reload`). Used in production to utilize multiple CPU cores.
- `--log-level info`: Configures log verbosity (`critical`, `error`, `warning`, `info`, `debug`, `trace`).

**Terminal Console Output:**
```text
INFO:     Will watch for changes in these directories: ['/fastapi-mastery']
INFO:     Uvicorn running on http://127.0.0.1:8000 (Press CTRL+C to quit)
INFO:     Started re-loader process [54321] using WatchFiles
INFO:     Started server process [54322]
INFO:     Waiting for application startup.
INFO:     Application startup complete.
```

### Multiple Endpoints Example & Console Output Walkthrough

Let's build a real multi-endpoint API to demonstrate how routing works:

```python
# main.py
from fastapi import FastAPI
from datetime import datetime

app = FastAPI(title="Company Directory API")

# Endpoint 1: Root Greeting
@app.get("/")
def home():
    return {"message": "Welcome to Acme Corp API"}

# Endpoint 2: System Health Check
@app.get("/health")
def health_check():
    return {
        "status": "healthy",
        "database": "connected",
        "timestamp": datetime.utcnow().isoformat()
    }

# Endpoint 3: Public Company Information
@app.get("/about")
def company_about():
    return {
        "company": "Acme Corporation",
        "founded": 2018,
        "headquarters": "San Francisco, CA",
        "technologies": ["FastAPI", "Python", "PostgreSQL", "Docker"]
    }
```

#### Testing the Endpoints with cURL & Inspecting Outputs:

##### Test Endpoint 1:
```bash
curl -i -X GET http://127.0.0.1:8000/
```
**HTTP Response Output:**
```http
HTTP/1.1 200 OK
date: Tue, 27 Oct 2026 14:15:30 GMT
server: uvicorn
content-length: 42
content-type: application/json

{"message":"Welcome to Acme Corp API"}
```

##### Test Endpoint 2:
```bash
curl -X GET http://127.0.0.1:8000/health
```
**JSON Response Output:**
```json
{
  "status": "healthy",
  "database": "connected",
  "timestamp": "2026-10-27T14:15:31.902341"
}
```

##### Uvicorn Terminal Logs:
Every time an incoming HTTP request hits your server, Uvicorn outputs a live colored access log:
```text
INFO:     127.0.0.1:58492 - "GET / HTTP/1.1" 200 OK
INFO:     127.0.0.1:58494 - "GET /health HTTP/1.1" 200 OK
INFO:     127.0.0.1:58496 - "GET /about HTTP/1.1" 200 OK
```

### Interactive Documentation: Swagger UI, ReDoc, and OpenAPI

Without writing extra documentation files, FastAPI automatically serves:
1. **Swagger UI (`http://127.0.0.1:8000/docs`):** Interactive browser GUI with live "Try it out" execution.
2. **ReDoc (`http://127.0.0.1:8000/redoc`):** Clean, publication-quality technical documentation.
3. **OpenAPI JSON (`http://127.0.0.1:8000/openapi.json`):** Machine-readable schema compliant with OpenAPI 3.1.

---

## Chapter 4: Path Operation Configuration, Metadata, Docs URLs & Static Files

### Configuring Tags, Summary, Description, and Deprecation

Path operation decorators accept rich metadata to structure the automatic documentation:

```python
from fastapi import FastAPI, status

app = FastAPI()

@app.get(
    "/items/{item_id}",
    tags=["Items Management"],
    summary="Retrieve Item by ID",
    description="Fetches full details of a specific inventory item from storage.",
    response_description="The fully populated item record",
    status_code=status.HTTP_200_OK,
    deprecated=False
)
def get_item(item_id: int):
    return {"item_id": item_id, "name": "Wireless Mouse", "price": 29.99}

@app.get("/legacy-items/", tags=["Items Management"], deprecated=True)
def get_legacy_items():
    """⚠️ Deprecated: Migrate to /items/ as soon as possible."""
    return [{"id": 1, "note": "Use new API"}]
```

### Customizing API Metadata, OpenAPI URL, and Disabling Docs

In security-hardened production environments, you can customize or disable the documentation endpoints:

```python
from fastapi import FastAPI

app = FastAPI(
    title="Acme Corp Enterprise API",
    description="""
    ## Welcome to Acme Corp API
    
    Here you can access:
    * **Users**: Identity management
    * **Orders**: Billing and fulfillment
    """,
    version="2.5.0",
    terms_of_service="https://example.com/terms/",
    contact={
        "name": "API Support Team",
        "url": "https://example.com/support",
        "email": "support@example.com",
    },
    license_info={
        "name": "Apache 2.0",
        "url": "https://www.apache.org/licenses/LICENSE-2.0.html",
    },
    # Set to None in production to disable public Swagger/ReDoc docs:
    docs_url="/api/documentation",  # Custom swagger URL
    redoc_url=None,                  # Disable ReDoc
    openapi_url="/api/schema.json"   # Custom schema URL
)
```

### Serving Static Files with StaticFiles

FastAPI can serve static assets (HTML, CSS, JavaScript, uploaded images) using Starlette's `StaticFiles`:

```python
from pathlib import Path
from fastapi import FastAPI
from fastapi.staticfiles import StaticFiles

app = FastAPI()

# Create static directory
STATIC_DIR = Path("./static")
STATIC_DIR.mkdir(exist_ok=True)

# Mount the static directory to /static
app.mount("/static", StaticFiles(directory="static"), name="static")

@app.get("/status")
def status_check():
    return {"static_url": "/static/styles.css"}
```

### Folder Layout for Static Assets

```text
my_fastapi_project/
├── main.py
├── static/
│   ├── css/
│   │   └── main.css
│   ├── js/
│   │   └── dashboard.js
│   ├── images/
│   │   └── logo.png
│   └── uploads/
│       └── avatars/
└── templates/
    └── index.html
```

---

# Module 2: Parameters, Validation & Advanced Request Data

---

## Chapter 5: Path Parameters and Numeric Validations

### Dynamic Path Routing & Type Hints

Path parameters capture values directly from the URL. Python type hints enforce automatic type conversion and validation:

```python
from fastapi import FastAPI, HTTPException

app = FastAPI()

DATABASE = {1: "Keyboard", 2: "Monitor", 3: "Desk Mat"}

@app.get("/products/{product_id}")
def read_product(product_id: int):
    if product_id not in DATABASE:
        raise HTTPException(status_code=404, detail="Product not found")
    return {"product_id": product_id, "name": DATABASE[product_id]}
```

### Enum Path Parameters (Strict Choice Validation)

Use Python `enum.Enum` to restrict URL paths to exact pre-approved choices:

```python
from enum import Enum
from fastapi import FastAPI

class ModelTier(str, Enum):
    BASIC = "basic"
    PRO = "pro"
    ENTERPRISE = "enterprise"

app = FastAPI()

@app.get("/plans/{tier}")
def get_plan(tier: ModelTier):
    if tier is ModelTier.BASIC:
        return {"tier": tier, "price_monthly": 0}
    elif tier is ModelTier.PRO:
        return {"tier": tier, "price_monthly": 29}
    return {"tier": tier, "price_monthly": 99}
```

In the Swagger UI (`/docs`), `tier` appears as a pre-populated dropdown menu containing only `basic`, `pro`, and `enterprise`.

### Numeric Validation with Path (ge, le, gt, lt)

Use `Path(...)` to enforce mathematical boundaries:

```python
from fastapi import FastAPI, Path

app = FastAPI()

@app.get("/accounts/{account_id}/transactions/{tx_id}")
def get_transaction(
    account_id: int = Path(..., title="Account ID", ge=1, le=1_000_000),
    tx_id: int = Path(..., title="Transaction ID", gt=0, description="Strictly positive transaction ID")
):
    return {"account_id": account_id, "tx_id": tx_id}
```

- `ge`: Greater than or equal to.
- `gt`: Strictly greater than.
- `le`: Less than or equal to.
- `lt`: Strictly less than.

### Path Parameter Order Matters

FastAPI evaluates routes sequentially from top to bottom. Specific fixed paths must be declared **before** dynamic path parameters:

```python
from fastapi import FastAPI

app = FastAPI()

# ✅ CORRECT: Declare fixed path FIRST
@app.get("/users/me")
def read_current_user():
    return {"user": "current_authenticated_user"}

# Declare dynamic path SECOND
@app.get("/users/{user_id}")
def read_user_by_id(user_id: int):
    return {"user_id": user_id}
```

> If `/users/{user_id}` were declared first, requests to `/users/me` would attempt to parse `"me"` as an integer `user_id` and fail with HTTP 422!

### Detailed Validation Error Outputs

When a client sends an invalid path parameter:
```bash
curl -X GET http://127.0.0.1:8000/accounts/-5/transactions/0
```
FastAPI automatically returns HTTP **422 Unprocessable Entity** with an array describing every failed constraint:

```json
{
  "detail": [
    {
      "type": "greater_than_equal",
      "loc": ["path", "account_id"],
      "msg": "Input should be greater than or equal to 1",
      "input": "-5",
      "ctx": {"ge": 1}
    },
    {
      "type": "greater_than",
      "loc": ["path", "tx_id"],
      "msg": "Input should be greater than 0",
      "input": "0",
      "ctx": {"gt": 0}
    }
  ]
}
```

---

## Chapter 6: Query Parameters and String Validations

### Query Parameters with Defaults and Optional Values

Parameters not defined in the URL path are automatically interpreted as URL Query Parameters (`?key=val`):

```python
from typing import Optional
from fastapi import FastAPI

app = FastAPI()

@app.get("/catalog/")
def get_catalog(
    page: int = 1,                 # Default value 1
    page_size: int = 20,           # Default value 20
    search: Optional[str] = None   # Optional parameter (defaults to None)
):
    return {"page": page, "page_size": page_size, "search": search}
```

### String Validations with Query (Length & Regex Patterns)

Use `Query(...)` to declare validation constraints:

```python
from typing import Optional
from fastapi import FastAPI, Query

app = FastAPI()

@app.get("/articles/")
def list_articles(
    q: Optional[str] = Query(
        None,
        min_length=3,
        max_length=50,
        pattern=r"^[a-zA-Z0-9_\s-]+$",
        title="Search Query",
        description="Search term (letters, numbers, hyphens, and underscores only)",
        examples=["fastapi tutorial"]
    )
):
    return {"query": q}
```

### Receiving Lists / Multiple Values in Query Parameters

To accept multiple query values with the same key (e.g. `?tag=python&tag=docker&tag=web`):

```python
from typing import List
from fastapi import FastAPI, Query

app = FastAPI()

@app.get("/filter-tags/")
def filter_by_tags(
    tags: List[str] = Query(
        default=["general"],
        description="Filter items by multiple category tags"
    )
):
    return {"selected_tags": tags}
```

**Testing via cURL:**
```bash
curl "http://127.0.0.1:8000/filter-tags/?tags=python&tags=fastapi&tags=backend"
```
**Output:**
```json
{"selected_tags":["python","fastapi","backend"]}
```

### Advanced Real-World Filtering Example (E-Commerce Catalog)

```python
from typing import List, Optional
from fastapi import FastAPI, Query

app = FastAPI()

INVENTORY = [
    {"id": 1, "title": "Mechanical Keyboard", "category": "electronics", "price": 120.0, "in_stock": True},
    {"id": 2, "title": "Ergonomic Chair", "category": "furniture", "price": 350.0, "in_stock": True},
    {"id": 3, "title": "Coffee Beans", "category": "groceries", "price": 18.0, "in_stock": False},
    {"id": 4, "title": "USB-C Cable", "category": "electronics", "price": 12.0, "in_stock": True},
    {"id": 5, "title": "Standing Desk", "category": "furniture", "price": 490.0, "in_stock": True},
]

@app.get("/search/products")
def search_products(
    min_price: float = Query(0.0, ge=0.0, description="Minimum price filter"),
    max_price: Optional[float] = Query(None, gt=0.0, description="Maximum price filter"),
    categories: Optional[List[str]] = Query(None, description="Select multiple categories"),
    only_in_stock: bool = Query(True, description="Filter only items currently in stock"),
    sort_by: str = Query("price", pattern="^(price|title)$")
):
    results = INVENTORY

    # 1. Filter by minimum price
    results = [item for item in results if item["price"] >= min_price]

    # 2. Filter by maximum price (if provided)
    if max_price is not None:
        results = [item for item in results if item["price"] <= max_price]

    # 3. Filter by categories (if provided)
    if categories:
        results = [item for item in results if item["category"] in categories]

    # 4. Filter by stock status
    if only_in_stock:
        results = [item for item in results if item["in_stock"]]

    # 5. Sort results
    results = sorted(results, key=lambda x: x[sort_by])

    return {"total_found": len(results), "products": results}
```

#### Test Request & Output:
```bash
curl "http://127.0.0.1:8000/search/products?min_price=10&max_price=200&categories=electronics&only_in_stock=true"
```
**Response JSON:**
```json
{
  "total_found": 2,
  "products": [
    {
      "id": 4,
      "title": "USB-C Cable",
      "category": "electronics",
      "price": 12.0,
      "in_stock": true
    },
    {
      "id": 1,
      "title": "Mechanical Keyboard",
      "category": "electronics",
      "price": 120.0,
      "in_stock": true
    }
  ]
}
```

---

## Chapter 7: Request Body, Pydantic Models & Field Validations

### What is Pydantic? Parsing vs Validation

Unlike standard Python dictionaries, Pydantic guarantees that data passing through your application adheres strictly to typed schema contracts:

```
Raw JSON String ---> [Pydantic Parsing & Coercion] ---> [Field Validation] ---> Validated Python Object
```

### Creating Schemas with BaseModel & Field

```python
from typing import Optional, List
from pydantic import BaseModel, Field, EmailStr
from fastapi import FastAPI, status

app = FastAPI()

class ItemSchema(BaseModel):
    name: str = Field(..., min_length=2, max_length=50, examples=["Ergonomic Desk"])
    description: Optional[str] = Field(None, max_length=300)
    price: float = Field(..., gt=0.0, description="Price must be strictly positive")
    tax: Optional[float] = Field(0.0, ge=0.0)
    tags: List[str] = Field(default_factory=list)

@app.post("/items/", status_code=status.HTTP_201_CREATED)
def create_item(item: ItemSchema):
    item_dict = item.model_dump()
    total_price = item.price + (item.tax or 0.0)
    item_dict["total_price"] = total_price
    return item_dict
```

### Pydantic V2 Custom Validators with @field_validator

```python
from pydantic import BaseModel, field_validator

class UserSignUp(BaseModel):
    username: str
    password: str

    @field_validator("username")
    @classmethod
    def validate_username(cls, value: str) -> str:
        if not value.isalnum():
            raise ValueError("Username must contain only alphanumeric characters")
        if len(value) < 4:
            raise ValueError("Username must be at least 4 characters long")
        return value.lower()

    @field_validator("password")
    @classmethod
    def validate_password_strength(cls, value: str) -> str:
        if len(value) < 8:
            raise ValueError("Password must be at least 8 characters long")
        if not any(char.isdigit() for char in value):
            raise ValueError("Password must contain at least one digit")
        return value
```

### Complete User Registration Schema Example

```python
from typing import Optional
from pydantic import BaseModel, EmailStr, Field, field_validator
from fastapi import FastAPI, status

app = FastAPI()

class RegistrationSchema(BaseModel):
    email: EmailStr = Field(..., description="Valid corporate or personal email")
    username: str = Field(..., min_length=3, max_length=30)
    password: str = Field(..., min_length=8)
    age: int = Field(..., ge=18, le=120, description="Must be 18 or older to register")
    phone_number: Optional[str] = Field(None, pattern=r"^\+?[1-9]\d{1,14}$")

    @field_validator("username")
    @classmethod
    def no_reserved_usernames(cls, v: str) -> str:
        reserved = ["admin", "root", "system", "moderator"]
        if v.lower() in reserved:
            raise ValueError(f"'{v}' is a reserved system username")
        return v.lower()

@app.post("/register", status_code=status.HTTP_201_CREATED)
def register(user: RegistrationSchema):
    return {
        "status": "success",
        "username": user.username,
        "email": user.email,
        "age": user.age
    }
```

---

## Chapter 8: Body - Multiple Parameters, Singular Values & Embedding

### Mixing Path, Query, and Body Parameters

FastAPI detects parameter roles automatically based on their declaration:
- In the path $\rightarrow$ **Path Parameter**
- Singular primitive type not in path $\rightarrow$ **Query Parameter**
- Pydantic model $\rightarrow$ **Request Body**

```python
from fastapi import FastAPI, Path, Query
from pydantic import BaseModel

app = FastAPI()

class Item(BaseModel):
    name: str
    price: float

@app.put("/items/{item_id}")
def update_item(
    item_id: int = Path(..., ge=1),           # Path parameter
    q: str = Query(None, min_length=3),       # Query parameter
    item: Item = None                         # Request Body
):
    return {"item_id": item_id, "q": q, "item": item}
```

### Multiple Pydantic Body Parameters

You can declare multiple Pydantic models in a single endpoint. FastAPI expects a JSON object containing keys matching each parameter name:

```python
from fastapi import FastAPI
from pydantic import BaseModel

app = FastAPI()

class User(BaseModel):
    username: str
    full_name: str

class Item(BaseModel):
    name: str
    price: float

@app.post("/checkout")
def process_checkout(user: User, item: Item):
    return {"buyer": user.username, "product": item.name}
```

**Expected JSON Body:**
```json
{
  "user": {
    "username": "alice",
    "full_name": "Alice Smith"
  },
  "item": {
    "name": "Noise Cancelling Headphones",
    "price": 199.99
  }
}
```

### Singular Values in Body with Body(...)

To accept a primitive value (like an `int` or `str`) from the JSON body instead of a query parameter, use `Body(...)`:

```python
from fastapi import FastAPI, Body

app = FastAPI()

@app.post("/verify-code")
def verify_code(
    user_id: int = Body(...),
    pin: int = Body(..., ge=1000, le=9999)
):
    return {"user_id": user_id, "pin_verified": True}
```

### Embed a Single Body Parameter with embed=True

By default, a single Pydantic model expects the raw JSON body to match its fields. If you want the body to be wrapped in a key:

```python
from fastapi import FastAPI, Body
from pydantic import BaseModel

app = FastAPI()

class Product(BaseModel):
    name: str
    price: float

# Expects: {"product": {"name": "Lamp", "price": 24.50}}
@app.post("/products/embed")
def create_embedded_product(product: Product = Body(..., embed=True)):
    return {"received_product": product}
```

---

## Chapter 9: Body - Nested Models, Deep Structures & Sets

### Nested Sub-Models

Pydantic models can be nested arbitrarily deep:

```python
from typing import List, Optional
from pydantic import BaseModel, HttpUrl
from fastapi import FastAPI

app = FastAPI()

class Image(BaseModel):
    url: HttpUrl
    caption: Optional[str] = None

class ItemWithImages(BaseModel):
    name: str
    description: Optional[str] = None
    price: float
    thumbnail: Image                    # Nested single model
    gallery: List[Image] = []           # Nested list of models

@app.post("/gallery-items/")
def create_gallery_item(item: ItemWithImages):
    return {"name": item.name, "image_count": len(item.gallery) + 1}
```

### Attributes with Lists and Sets for Uniqueness

Use `Set[str]` when values must be unique (Pydantic automatically deduplicates incoming arrays):

```python
from typing import Set
from pydantic import BaseModel
from fastapi import FastAPI

app = FastAPI()

class TaggedArticle(BaseModel):
    title: str
    tags: Set[str] = set()

@app.post("/articles/")
def create_article(article: TaggedArticle):
    # If client sends ["python", "api", "python"], article.tags is {'python', 'api'}
    return {"title": article.title, "unique_tags": list(article.tags)}
```

### Deeply Nested Models and Dictionaries with Arbitrary Keys

When keys cannot be predefined in advance (e.g. dynamic metadata or translations):

```python
from typing import Dict
from pydantic import BaseModel
from fastapi import FastAPI

app = FastAPI()

class DynamicPayload(BaseModel):
    event_name: str
    translations: Dict[str, str]        # e.g. {"en": "Hello", "es": "Hola"}
    metric_scores: Dict[str, float]     # e.g. {"accuracy": 0.94, "loss": 0.06}

@app.post("/events")
def record_event(payload: DynamicPayload):
    return {"event": payload.event_name, "supported_locales": list(payload.translations.keys())}
```

### Complete Order & Line-Item Invoice Example

```python
from typing import List
from pydantic import BaseModel, Field, EmailStr
from fastapi import FastAPI, status

app = FastAPI()

class Address(BaseModel):
    street: str
    city: str
    zip_code: str
    country: str = "USA"

class LineItem(BaseModel):
    sku: str = Field(..., min_length=4)
    description: str
    unit_price: float = Field(..., gt=0)
    quantity: int = Field(..., ge=1)

class Customer(BaseModel):
    full_name: str
    email: EmailStr
    shipping_address: Address

class Invoice(BaseModel):
    invoice_number: str
    customer: Customer
    items: List[LineItem]
    notes: str = ""

@app.post("/invoices/", status_code=status.HTTP_201_CREATED)
def submit_invoice(invoice: Invoice):
    subtotal = sum(item.unit_price * item.quantity for item in invoice.items)
    tax = subtotal * 0.08
    grand_total = subtotal + tax

    return {
        "invoice_number": invoice.invoice_number,
        "recipient": invoice.customer.full_name,
        "shipping_city": invoice.customer.shipping_address.city,
        "item_count": sum(i.quantity for i in invoice.items),
        "subtotal": round(subtotal, 2),
        "tax": round(tax, 2),
        "total_due": round(grand_total, 2)
    }
```

---

## Chapter 10: Extra Data Types

FastAPI natively supports advanced standard-library Python types:

```python
from uuid import UUID, uuid4
from datetime import datetime, date, time, timedelta
from decimal import Decimal
from fastapi import FastAPI, Body

app = FastAPI()

@app.post("/contracts/{contract_id}")
def create_contract(
    contract_id: UUID,
    start_date: date = Body(...),
    daily_start_time: time = Body(...),
    duration: timedelta = Body(...),
    hourly_rate: Decimal = Body(...),
    created_at: datetime = Body(default_factory=datetime.utcnow)
):
    end_date = start_date + duration
    return {
        "contract_id": str(contract_id),
        "start_date": start_date.isoformat(),
        "estimated_completion": end_date.isoformat(),
        "duration_days": duration.days,
        "hourly_rate": str(hourly_rate),
        "created_at": created_at.isoformat()
    }
```

| Type | Accepted String Input Format | Output Serialized Format |
| :--- | :--- | :--- |
| `UUID` | `"a1b2c3d4-e5f6-7890-1234-56789abcdef0"` | Standard UUID string |
| `datetime` | ISO-8601 string (`"2026-10-27T14:30:00Z"`) | ISO-8601 string |
| `date` | `"2026-10-27"` | ISO-8601 date string |
| `time` | `"14:30:00"` | ISO-8601 time string |
| `timedelta` | Number of seconds or ISO duration (`3600`) | Float (total seconds) |
| `Decimal` | Number or numeric string (`"19.99"`) | Float/Decimal representation |

### Complete SaaS Subscription Billing Model Example

```python
from uuid import UUID, uuid4
from datetime import date, timedelta
from decimal import Decimal
from pydantic import BaseModel, Field
from fastapi import FastAPI, status

app = FastAPI()

class SubscriptionPlan(BaseModel):
    user_id: UUID
    plan_name: str
    monthly_rate: Decimal = Field(..., decimal_places=2, max_digits=8)
    trial_period: timedelta = Field(default=timedelta(days=14))
    start_date: date = Field(default_factory=date.today)

@app.post("/subscriptions/", status_code=status.HTTP_201_CREATED)
def create_subscription(sub: SubscriptionPlan):
    billing_commences = sub.start_date + sub.trial_period
    return {
        "subscription_id": str(uuid4()),
        "user_id": str(sub.user_id),
        "plan": sub.plan_name,
        "monthly_charge_usd": str(sub.monthly_rate),
        "trial_days": sub.trial_period.days,
        "first_billing_date": billing_commences.isoformat()
    }
```

---

## Chapter 11: Cookie & Header Parameters (Individual & Pydantic Models)

### Reading Cookies with Cookie(...)

```python
from typing import Optional
from fastapi import FastAPI, Cookie

app = FastAPI()

@app.get("/session")
def read_session_cookie(
    session_token: Optional[str] = Cookie(None),
    tracking_id: Optional[str] = Cookie(None)
):
    return {"session_token": session_token, "tracking_id": tracking_id}
```

### Reading Headers with Header(...)

FastAPI automatically converts HTTP headers like `User-Agent` into Python snake_case `user_agent`:

```python
from typing import Optional, List
from fastapi import FastAPI, Header

app = FastAPI()

@app.get("/headers-demo")
def read_headers(
    user_agent: Optional[str] = Header(None),
    accept_language: Optional[str] = Header(None),
    x_api_key: Optional[str] = Header(None, alias="X-Api-Key"),
    x_custom_tags: Optional[List[str]] = Header(None)  # Multi-value headers
):
    return {
        "User-Agent": user_agent,
        "Accept-Language": accept_language,
        "X-Api-Key": x_api_key,
        "Custom-Tags": x_custom_tags
    }
```

### Query Parameter Models

In modern FastAPI, you can group related query parameters into a clean Pydantic model using `Query()`:

```python
from typing import Optional
from pydantic import BaseModel, Field
from fastapi import FastAPI, Query

app = FastAPI()

class FilterParams(BaseModel):
    limit: int = Field(10, ge=1, le=100)
    offset: int = Field(0, ge=0)
    order_by: str = Field("created_at")
    search: Optional[str] = None

@app.get("/catalog-items")
def get_catalog_items(filters: FilterParams = Query()):
    return {"filters_applied": filters.model_dump()}
```

**Testing via cURL:**
```bash
curl "http://127.0.0.1:8000/catalog-items?limit=25&offset=50&order_by=price"
```

### Cookie Parameter Models & Header Parameter Models

```python
from typing import Optional
from pydantic import BaseModel
from fastapi import FastAPI, Header, Cookie

app = FastAPI()

class HeaderSecuritySchema(BaseModel):
    user_agent: Optional[str] = None
    x_auth_client: Optional[str] = None

class CookieTrackingSchema(BaseModel):
    session_id: Optional[str] = None
    consent_accepted: bool = False

@app.get("/secure-telemetry")
def telemetry(
    headers: HeaderSecuritySchema = Header(),
    cookies: CookieTrackingSchema = Cookie()
):
    return {"headers": headers.model_dump(), "cookies": cookies.model_dump()}
```

---

## Chapter 12: Request Forms, File Uploads, Form Models & Combined Requests

### Form Data with Form(...)

```bash
pip install python-multipart
```

```python
from fastapi import FastAPI, Form

app = FastAPI()

@app.post("/login-form")
def handle_form_login(
    username: str = Form(...),
    password: str = Form(...)
):
    return {"user": username, "source": "HTML Form Submission"}
```

### File Uploads: bytes vs UploadFile

```
Comparison: bytes vs UploadFile
+-------------------+-----------------------------------+-----------------------------------+
| Feature           | bytes (File(...))                 | UploadFile (File(...))            |
+-------------------+-----------------------------------+-----------------------------------+
| Storage Location  | Entire file read directly to RAM  | Spooled on disk (safe for memory) |
| Max File Size     | Small files (< 5 MB)              | Gigabytes without OOM crashes     |
| File Operations   | In-memory raw bytes               | Standard async file stream        |
| Metadata Access   | None                              | filename, content_type, headers   |
+-------------------+-----------------------------------+-----------------------------------+
```

```python
import shutil
from pathlib import Path
from fastapi import FastAPI, UploadFile, File, HTTPException

app = FastAPI()
STORAGE_DIR = Path("./media")
STORAGE_DIR.mkdir(exist_ok=True)

@app.post("/upload-document/")
async def upload_document(file: UploadFile = File(...)):
    if not file.filename.endswith((".pdf", ".docx")):
        raise HTTPException(status_code=400, detail="Only PDF and DOCX documents allowed")
    
    target_path = STORAGE_DIR / file.filename
    with target_path.open("wb") as buffer:
        shutil.copyfileobj(file.file, buffer)
        
    return {
        "filename": file.filename,
        "content_type": file.content_type,
        "saved_path": str(target_path)
    }
```

### Combining Form Fields and Uploaded Files in One Request

```python
from fastapi import FastAPI, Form, File, UploadFile

app = FastAPI()

@app.post("/create-profile")
async def create_user_profile(
    display_name: str = Form(...),
    bio: str = Form(None),
    avatar: UploadFile = File(...)
):
    return {
        "display_name": display_name,
        "bio": bio,
        "avatar_filename": avatar.filename,
        "avatar_mime": avatar.content_type
    }
```

### Uploading Multiple Files Simultaneously (List[UploadFile])

```python
from typing import List
from fastapi import FastAPI, File, UploadFile

app = FastAPI()

@app.post("/upload-multiple-photos/")
async def upload_multiple_photos(photos: List[UploadFile] = File(...)):
    uploaded_manifest = []
    for photo in photos:
        uploaded_manifest.append({
            "name": photo.filename,
            "size_bytes": photo.size,
            "type": photo.content_type
        })
    return {"total_uploaded": len(photos), "files": uploaded_manifest}
```

### Request Form Models (Pydantic Models as Forms)

In modern FastAPI, you can bind an entire Pydantic model directly to HTML form data using `Form()`:

```python
from pydantic import BaseModel
from fastapi import FastAPI, Form

app = FastAPI()

class RegistrationFormData(BaseModel):
    username: str
    email: str
    age: int

@app.post("/register-client")
def register_client(form_data: RegistrationFormData = Form()):
    return {"registered": form_data.model_dump()}
```

---

# Module 3: Response Modeling, Error Handling & Data Transformation

---

## Chapter 13: Response Status Codes & Path Configuration

### Explicit HTTP Status Codes with fastapi.status

Always use the symbolic constants from `fastapi.status`:

```python
from fastapi import FastAPI, status

app = FastAPI()

@app.delete("/records/{record_id}", status_code=status.HTTP_204_NO_CONTENT)
def purge_record(record_id: int):
    # 204 No Content means success with an empty HTTP response body
    return None
```

### Setting Status Codes Dynamically with Response

When the return status code depends on dynamic business logic:

```python
from fastapi import FastAPI, Response, status

app = FastAPI()

@app.post("/orders/{order_id}/cancel")
def cancel_order(order_id: int, response: Response):
    if order_id == 100:
        response.status_code = status.HTTP_200_OK
        return {"status": "Order cancelled, refund initiated"}
    
    response.status_code = status.HTTP_202_ACCEPTED
    return {"status": "Cancellation request queued for review"}
```

---

## Chapter 14: Response Models & Return Type Annotations

### Data Filtering & Security: Why Response Models are Mandatory

**Security Principle:** Internal database rows contain sensitive attributes (e.g. `hashed_password`, internal billing IDs, admin flags). A `response_model` ensures that only explicitly defined public attributes are ever transmitted to the client.

```python
from pydantic import BaseModel, EmailStr
from fastapi import FastAPI, status

app = FastAPI()

class UserInput(BaseModel):
    username: str
    email: EmailStr
    password: str

class UserOutput(BaseModel):
    id: int
    username: str
    email: EmailStr

DATABASE = {}

@app.post("/users/", response_model=UserOutput, status_code=status.HTTP_201_CREATED)
def register(user: UserInput):
    user_id = len(DATABASE) + 1
    stored_row = {
        "id": user_id,
        "username": user.username,
        "email": user.email,
        "hashed_password": "bcrypt$secret$" + user.password,
        "internal_admin_notes": "Registered via web campaign"
    }
    DATABASE[user_id] = stored_row
    # FastAPI filters out 'hashed_password' and 'internal_admin_notes' automatically!
    return stored_row
```

### Return Type vs response_model

In modern FastAPI, you can use standard Python return type annotations:

```python
@app.get("/users/{user_id}")
def get_user_profile(user_id: int) -> UserOutput:
    return UserOutput(id=user_id, username="alice", email="alice@example.com")
```

Use `response_model=UserOutput` when your function returns a dictionary or an ORM database object, and you want FastAPI to convert and filter it into the schema.

### Filtering Out Unset Data with response_model_exclude_unset

```python
from typing import Optional
from pydantic import BaseModel
from fastapi import FastAPI

app = FastAPI()

class ItemView(BaseModel):
    name: str
    description: Optional[str] = None
    price: float
    tax: float = 1.5

# exclude_unset=True strips default values that were not explicitly set by the handler!
@app.get("/sparse-items", response_model=ItemView, response_model_exclude_unset=True)
def get_sparse_item():
    return {"name": "Coffee Mug", "price": 12.0}
```

---

## Chapter 15: Extra Models & Inheritance Patterns

### Model Inheritance: Base, Create, InDB, and Public Response

Prevent schema code duplication by establishing a clean class hierarchy:

```
                  +-------------------+
                  |     ItemBase      |  (Shared: title, description, price)
                  +-------------------+
                       /         \
                      v           v
       +------------------+    +-------------------+
       |    ItemCreate    |    |     ItemInDB      |
       | (Same as Base)   |    | (+ id, created_at,|
       +------------------+    |    owner_id)      |
                               +-------------------+
                                         |
                                         v
                               +-------------------+
                               |   ItemResponse    |
                               | (+ id, created_at)|
                               +-------------------+
```

```python
from datetime import datetime
from typing import Optional
from pydantic import BaseModel, ConfigDict
from fastapi import FastAPI

app = FastAPI()

class ItemBase(BaseModel):
    title: str
    description: Optional[str] = None
    price: float

class ItemCreate(ItemBase):
    pass

class ItemUpdate(BaseModel):
    title: Optional[str] = None
    price: Optional[float] = None

class ItemInDB(ItemBase):
    id: int
    owner_id: int
    created_at: datetime
    internal_margin: float

class ItemResponse(ItemBase):
    id: int
    created_at: datetime
    
    model_config = ConfigDict(from_attributes=True)
```

### Union Types for Polymorphic Response Models

When an endpoint can return different schema structures based on business conditions:

```python
from typing import Union
from pydantic import BaseModel
from fastapi import FastAPI

app = FastAPI()

class Car(BaseModel):
    brand: str
    passengers: int

class Plane(BaseModel):
    brand: str
    wingspan_meters: float

@app.get("/vehicles/{vehicle_type}", response_model=Union[Car, Plane])
def get_vehicle(vehicle_type: str):
    if vehicle_type == "plane":
        return Plane(brand="Boeing", wingspan_meters=64.8)
    return Car(brand="Tesla", passengers=5)
```

### Schema Extra & OpenAPI Documentation Examples

Provide realistic example payloads directly inside the Swagger documentation:

```python
from pydantic import BaseModel, Field, ConfigDict

class ProductSchema(BaseModel):
    title: str = Field(..., examples=["Mechanical Keyboard"])
    price: float = Field(..., examples=[149.99])

    model_config = ConfigDict(
        json_schema_extra={
            "examples": [
                {
                    "title": "Ergonomic Split Keyboard",
                    "price": 289.00
                }
            ]
        }
    )
```

---

## Chapter 16: Handling Errors & Custom Exception Handlers

### Raising HTTPException with Headers and Structured Details

```python
from fastapi import FastAPI, HTTPException, status

app = FastAPI()

@app.get("/accounts/{account_id}")
def fetch_account(account_id: int):
    if account_id == 0:
        raise HTTPException(
            status_code=status.HTTP_400_BAD_REQUEST,
            detail="Account ID 0 is reserved for system administration"
        )
    if account_id < 0:
        raise HTTPException(
            status_code=status.HTTP_404_NOT_FOUND,
            detail={"error_code": "INVALID_ACCOUNT", "entered": account_id},
            headers={"X-Error-Reason": "Negative ID disallowed"}
        )
    return {"account_id": account_id, "balance": 1500.0}
```

### Custom Domain Exceptions & Global Handlers with @app.exception_handler

```python
from fastapi import FastAPI, Request, status
from fastapi.responses import JSONResponse

class InsufficientFundsException(Exception):
    def __init__(self, requested: float, available: float):
        self.requested = requested
        self.available = available

app = FastAPI()

@app.exception_handler(InsufficientFundsException)
async def insufficient_funds_handler(request: Request, exc: InsufficientFundsException):
    return JSONResponse(
        status_code=status.HTTP_402_PAYMENT_REQUIRED,
        content={
            "error": "INSUFFICIENT_FUNDS",
            "requested_amount": exc.requested,
            "available_balance": exc.available,
            "message": f"Requested ${exc.requested}, but balance is only ${exc.available}"
        }
    )

@app.post("/transfer")
def transfer_money(amount: float):
    current_balance = 100.0
    if amount > current_balance:
        raise InsufficientFundsException(requested=amount, available=current_balance)
    return {"status": "success", "remaining_balance": current_balance - amount}
```

### Overriding Default Validation Error Handlers

To replace FastAPI's default HTTP 422 JSON payload with a custom format:

```python
from fastapi import FastAPI, Request, status
from fastapi.exceptions import RequestValidationError
from fastapi.responses import JSONResponse

app = FastAPI()

@app.exception_handler(RequestValidationError)
async def validation_exception_handler(request: Request, exc: RequestValidationError):
    errors = []
    for error in exc.errors():
        errors.append({
            "field": ".".join(str(loc) for loc in error["loc"]),
            "issue": error["msg"]
        })
    return JSONResponse(
        status_code=status.HTTP_400_BAD_REQUEST,
        content={"success": False, "validation_errors": errors}
    )
```

---

## Chapter 17: JSON Compatible Encoder & Data Updates (PUT vs PATCH)

### The Magic of jsonable_encoder

Non-primitive Python objects (such as `datetime`, `UUID`, sets, and Pydantic models) cannot be stored in databases or serialized by standard `json.dumps()`:

```python
from datetime import datetime
from uuid import uuid4
from fastapi.encoders import jsonable_encoder

data = {
    "id": uuid4(),
    "timestamp": datetime.utcnow(),
    "tags": {"fastapi", "python"}
}

# Converts UUID -> str, datetime -> ISO string, set -> list
json_ready = jsonable_encoder(data)
print(type(json_ready["id"]), json_ready["id"])
print(type(json_ready["timestamp"]), json_ready["timestamp"])
print(type(json_ready["tags"]), json_ready["tags"])
```

### Full Replacement with PUT vs Partial Update with PATCH

```
+--------+------------------+-----------------------------------------------------+
| Method | Semantic Action  | Behavior                                            |
+--------+------------------+-----------------------------------------------------+
| PUT    | Full Replacement | Unspecified attributes are overwritten with null/defaults|
| PATCH  | Partial Update   | Only fields sent by the client are modified         |
+--------+------------------+-----------------------------------------------------+
```

### Using model_dump(exclude_unset=True) for Patching

```python
from typing import Optional
from pydantic import BaseModel
from fastapi import FastAPI, HTTPException

app = FastAPI()

class ItemSchema(BaseModel):
    name: str
    price: float
    description: Optional[str] = None

class ItemPatch(BaseModel):
    name: Optional[str] = None
    price: Optional[float] = None
    description: Optional[str] = None

DB = {1: {"name": "Laptop", "price": 999.0, "description": "High performance"}}

@app.patch("/items/{item_id}")
def patch_item(item_id: int, patch: ItemPatch):
    if item_id not in DB:
        raise HTTPException(status_code=404, detail="Item not found")
        
    existing_item = DB[item_id]
    
    # exclude_unset=True captures ONLY fields sent in the HTTP request payload!
    patch_data = patch.model_dump(exclude_unset=True)
    
    # Update existing record in-place
    existing_item.update(patch_data)
    return {"status": "updated", "item": existing_item}
```

---

# Module 4: Dependency Injection, Middleware & Bigger Applications

---

## Chapter 18: Dependency Injection Fundamentals

### The Mental Model of Dependency Injection (The Hollywood Principle)

**"Don't call us, we'll call you."** Instead of having each endpoint instantiate database connections, security checks, and configuration parsers manually, FastAPI's **Dependency Injection (DI)** engine resolves the dependency tree automatically:

```
Without DI (Tight Coupling):
[ Endpoint Function ] ---> Creates DB Connection ---> Reads Config ---> Validates Token

With DI (FastAPI Depends):
             [ Dependency Graph Engine ]
              /           |           \
             v            v            v
     [ DB Connection ] [ App Config ] [ Authenticated User ]
              \           |           /
               v          v          v
                 [ Endpoint Function ]
```

```mermaid
flowchart TD
    Request["Incoming HTTP Request"] --> Router["FastAPI Router"]
    Router --> DI["Dependency Resolution Engine"]
    
    subgraph Dependencies["Resolved in Parallel / Order"]
        DB["get_db: SessionLocal"]
        Auth["get_current_user: JWT Token Decode"]
        Config["get_settings: AppConfig"]
    end
    
    DI --> DB
    DI --> Auth
    DI --> Config
    
    DB --> Endpoint["Endpoint: def update_profile(...)"]
    Auth --> Endpoint
    Config --> Endpoint
    
    Endpoint --> Response["Outgoing HTTP Response"]
```

### Function Dependencies with Depends(...)

```python
from typing import Optional
from fastapi import FastAPI, Depends

app = FastAPI()

def pagination_params(skip: int = 0, limit: int = 20):
    return {"skip": skip, "limit": limit}

@app.get("/users")
def get_users(pagination: dict = Depends(pagination_params)):
    return {"users": [], "pagination": pagination}
```

### Classes as Dependencies (Object-Oriented Injection)

Python classes can be used as dependencies directly:

```python
from fastapi import FastAPI, Depends

app = FastAPI()

class CommonQueryParams:
    def __init__(self, q: str = None, skip: int = 0, limit: int = 50):
        self.q = q
        self.skip = skip
        self.limit = limit

# Shortcut: Depends(CommonQueryParams) or even Depends() when type hinted!
@app.get("/items")
def read_items(params: CommonQueryParams = Depends()):
    return {"query": params.q, "range": f"{params.skip} to {params.skip + params.limit}"}
```

### Sub-dependencies: Resolving Hierarchical Dependency Graphs

Dependencies can depend on other dependencies:

```python
from fastapi import FastAPI, Depends, Header, HTTPException

app = FastAPI()

def get_api_key(x_api_key: str = Header(...)):
    if x_api_key != "secret-token-123":
        raise HTTPException(status_code=403, detail="Invalid API Key")
    return x_api_key

def get_authorized_user(api_key: str = Depends(get_api_key)):
    # Resolves get_api_key FIRST, then provides output here
    return {"user_id": 42, "role": "admin"}

@app.get("/admin/dashboard")
def view_dashboard(user: dict = Depends(get_authorized_user)):
    return {"status": "authorized", "user": user}
```

---

## Chapter 19: Advanced Dependencies: Decorators, Global & Yield Lifecycles

### Dependencies in Path Operation Decorators

When a dependency performs authentication or logging, but the endpoint does **not** need to receive its return value:

```python
from fastapi import FastAPI, Depends, Header, HTTPException

app = FastAPI()

def verify_internal_header(x_internal_token: str = Header(...)):
    if x_internal_token != "internal-cluster-only":
        raise HTTPException(status_code=400, detail="X-Internal-Token header invalid")

@app.get("/internal/health", dependencies=[Depends(verify_internal_header)])
def internal_health_check():
    return {"status": "ok", "cluster": "east-1"}
```

### Global Application Dependencies

To protect every single endpoint in your entire API application:

```python
from fastapi import FastAPI, Depends

def global_rate_limiter():
    # Execute rate limiting logic across every incoming request
    pass

app = FastAPI(dependencies=[Depends(global_rate_limiter)])
```

### Dependencies with yield (Setup & Teardown Context)

Essential for managing database sessions, file locks, and network resources:

```python
from fastapi import FastAPI, Depends

app = FastAPI()

def get_db_session():
    print(">>> [Resource] 1. Opening connection pool...")
    session = {"id": 101, "status": "active"}
    try:
        # Code before yield runs BEFORE the route handler
        yield session
    finally:
        # Code after yield runs AFTER the response is sent to the client!
        print(">>> [Resource] 2. Closing connection & releasing lock.")

@app.get("/orders")
def list_orders(db: dict = Depends(get_db_session)):
    print(f"Executing query with session #{db['id']}")
    return [{"order_id": 1}]
```

---

## Chapter 20: Middleware & CORS

### The Middleware Onion Architecture

A middleware is a function that executes around every request/response cycle:

```
       HTTP Request
            |
            v
   +-----------------+
   |   Middleware 1  |  (e.g., Timing Tracker)
   |  +------------+ |
   |  | Middleware 2 |  (e.g., CORS Header Check)
   |  |  +-------+ | |
   |  |  | Route | | |  (Your FastAPI Endpoint)
   |  |  +-------+ | |
   |  +------------+ |
   +-----------------+
            |
            v
       HTTP Response
```

### Custom Timing & Logging Middleware

```python
import time
from fastapi import FastAPI, Request

app = FastAPI()

@app.middleware("http")
async def add_process_time_header(request: Request, call_next):
    start_time = time.perf_counter()
    
    # Delegate to next middleware or path operation
    response = await call_next(request)
    
    execution_duration = time.perf_counter() - start_time
    response.headers["X-Process-Time-Sec"] = f"{execution_duration:.6f}"
    return response
```

### CORS (Cross-Origin Resource Sharing) Configuration

When frontends running on other domains (e.g. `http://localhost:3000`) communicate with your API:

```python
from fastapi import FastAPI
from fastapi.middleware.cors import CORSMiddleware

app = FastAPI()

origins = [
    "http://localhost:3000",
    "https://production-store.com"
]

app.add_middleware(
    CORSMiddleware,
    allow_origins=origins,             # Permitted client origins
    allow_credentials=True,            # Allow cookies / Authorization headers
    allow_methods=["*"],               # Allow all HTTP methods (GET, POST, etc.)
    allow_headers=["*"],               # Allow all headers
)
```

---

## Chapter 21: Background Tasks

### Running Operations in the Background

Use `BackgroundTasks` to perform non-blocking work after returning the HTTP response:

```python
import time
from fastapi import FastAPI, BackgroundTasks

app = FastAPI()

def send_receipt_email(email: str, order_id: int):
    time.sleep(2.0)  # Simulate slow SMTP network transmission
    print(f"Receipt for Order #{order_id} delivered to {email}")

@app.post("/orders/checkout")
def checkout(email: str, order_id: int, tasks: BackgroundTasks):
    tasks.add_task(send_receipt_email, email=email, order_id=order_id)
    # Delivered immediately to client (< 5ms)!
    return {"message": "Order placed successfully! Receipt will be emailed shortly."}
```

### Injecting BackgroundTasks into Endpoints & Dependencies

You can also attach background tasks inside dependencies:

```python
from fastapi import FastAPI, Depends, BackgroundTasks

app = FastAPI()

def audit_logger(background_tasks: BackgroundTasks):
    def log(message: str):
        background_tasks.add_task(print, f"[AUDIT LOG]: {message}")
    return log

@app.delete("/items/{item_id}")
def delete_item(item_id: int, logger=Depends(audit_logger)):
    logger(f"Item #{item_id} permanently deleted")
    return {"status": "deleted"}
```

---

## Chapter 22: Structuring Bigger Applications with APIRouter

### Why APIRouter is Essential for Real-World Codebases

Writing an entire application in a single `main.py` becomes unmaintainable. `APIRouter` lets you modularize endpoints into dedicated route controllers.

### Modular Directory Structure: Complete File Walkthrough

```text
my_fastapi_app/
├── app/
│   ├── __init__.py
│   ├── main.py              # Application factory & router mounts
│   ├── core/
│   │   ├── config.py        # Settings and environment variables
│   │   └── security.py      # Password hashing & JWT helpers
│   ├── db/
│   │   ├── database.py      # Session engine
│   │   └── models.py        # SQLAlchemy / SQLModel models
│   ├── schemas/             # Pydantic schemas
│   │   ├── user.py
│   │   └── product.py
│   └── routers/             # Controller endpoints
│       ├── users.py
│       └── products.py
└── requirements.txt
```

### Prefixes, Tags, and Nested Sub-Routers

#### 1. Define Router: `app/routers/products.py`
```python
from fastapi import APIRouter, HTTPException

router = APIRouter(
    prefix="/products",
    tags=["Products Management"]
)

@router.get("/")
def list_products():
    return [{"id": 1, "name": "Keyboard"}]

@router.get("/{product_id}")
def get_product(product_id: int):
    return {"id": product_id, "name": "Keyboard"}
```

#### 2. Include in Main App: `app/main.py`
```python
from fastapi import FastAPI
from app.routers import products

app = FastAPI(title="Modular Store API")

# Mount router with automatic prefix inclusion
app.include_router(products.router)
```

Now `GET /products/` and `GET /products/42` are registered automatically.

---

# Module 5: Databases & Data Management (SQLAlchemy & SQLModel)

---

## Chapter 23: Introduction to Relational Databases (SQLite & PostgreSQL)

### Database Concepts for API Developers

- **Table:** A collection of related data records organized into rows and columns.
- **Primary Key (PK):** Unique identifier for each row (`id`).
- **Foreign Key (FK):** Links a record in one table to the primary key of another table (`owner_id` $\rightarrow$ `users.id`).
- **Index:** A data structure that accelerates search queries on indexed columns.

### SQLite vs PostgreSQL Comparison

```
+--------------------+-----------------------------+-----------------------------+
| Feature            | SQLite                      | PostgreSQL                  |
+--------------------+-----------------------------+-----------------------------+
| Architecture       | Embedded serverless file    | Client-Server daemon engine |
| Setup Complexity   | Zero configuration          | Requires user authentication|
| Best For           | Local testing, mobile apps  | High-concurrency production |
| Concurrency Model  | Locks file on write         | Row-level MVCC concurrency  |
| Connection String  | sqlite:///./dev.db          | postgresql+psycopg2://...   |
+--------------------+-----------------------------+-----------------------------+
```

---

## Chapter 24: Modern SQLAlchemy 2.0 Integration & Full CRUD

### SQLAlchemy 2.0 Declarative Base, Mapped, and mapped_column

SQLAlchemy 2.0 introduced modern, fully type-safe model declarations using Python type annotations:

```python
# models.py
from datetime import datetime
from sqlalchemy import Integer, String, Float, ForeignKey, DateTime
from sqlalchemy.orm import DeclarativeBase, Mapped, mapped_column, relationship

class Base(DeclarativeBase):
    pass

class User(Base):
    __tablename__ = "users"

    id: Mapped[int] = mapped_column(Integer, primary_key=True, index=True)
    email: Mapped[str] = mapped_column(String(120), unique=True, index=True, nullable=False)
    created_at: Mapped[datetime] = mapped_column(DateTime, default=datetime.utcnow)

    products: Mapped[list["Product"]] = relationship(back_populates="owner")

class Product(Base):
    __tablename__ = "products"

    id: Mapped[int] = mapped_column(Integer, primary_key=True, index=True)
    title: Mapped[str] = mapped_column(String(100), index=True, nullable=False)
    price: Mapped[float] = mapped_column(Float, nullable=False)
    owner_id: Mapped[int] = mapped_column(Integer, ForeignKey("users.id"))

    owner: Mapped[User] = relationship(back_populates="products")
```

### Database Engine, SessionLocal, and get_db Dependency

```python
# database.py
from sqlalchemy import create_engine
from sqlalchemy.orm import sessionmaker

SQLALCHEMY_DATABASE_URL = "sqlite:///./app_database.db"

engine = create_engine(
    SQLALCHEMY_DATABASE_URL,
    connect_args={"check_same_thread": False}  # Only for SQLite!
)

SessionLocal = sessionmaker(autocommit=False, autoflush=False, bind=engine)

def get_db():
    db = SessionLocal()
    try:
        yield db
    finally:
        db.close()
```

### Full End-to-End CRUD Implementation (Create, Read, Update, Delete)

```python
from typing import List, Optional
from fastapi import FastAPI, Depends, HTTPException, status
from pydantic import BaseModel, ConfigDict
from sqlalchemy.orm import Session
from sqlalchemy import select

from database import engine, get_db
from models import Base, Product

# Create tables
Base.metadata.create_all(bind=engine)

app = FastAPI()

# Pydantic Schemas
class ProductCreate(BaseModel):
    title: str
    price: float

class ProductPatch(BaseModel):
    title: Optional[str] = None
    price: Optional[float] = None

class ProductResponse(BaseModel):
    id: int
    title: str
    price: float
    owner_id: int
    model_config = ConfigDict(from_attributes=True)

# 1. CREATE
@app.post("/products/", response_model=ProductResponse, status_code=status.HTTP_201_CREATED)
def create_product(product_in: ProductCreate, db: Session = Depends(get_db)):
    db_product = Product(**product_in.model_dump(), owner_id=1)
    db.add(db_product)
    db.commit()
    db.refresh(db_product)
    return db_product

# 2. READ ALL
@app.get("/products/", response_model=List[ProductResponse])
def list_products(skip: int = 0, limit: int = 20, db: Session = Depends(get_db)):
    stmt = select(Product).offset(skip).limit(limit)
    return db.scalars(stmt).all()

# 3. READ ONE
@app.get("/products/{product_id}", response_model=ProductResponse)
def get_product(product_id: int, db: Session = Depends(get_db)):
    stmt = select(Product).where(Product.id == product_id)
    product = db.scalars(stmt).first()
    if not product:
        raise HTTPException(status_code=404, detail="Product not found")
    return product

# 4. UPDATE (PATCH)
@app.patch("/products/{product_id}", response_model=ProductResponse)
def update_product(product_id: int, patch: ProductPatch, db: Session = Depends(get_db)):
    stmt = select(Product).where(Product.id == product_id)
    product = db.scalars(stmt).first()
    if not product:
        raise HTTPException(status_code=404, detail="Product not found")

    update_fields = patch.model_dump(exclude_unset=True)
    for key, value in update_fields.items():
        setattr(product, key, value)

    db.commit()
    db.refresh(product)
    return product

# 5. DELETE
@app.delete("/products/{product_id}", status_code=status.HTTP_204_NO_CONTENT)
def delete_product(product_id: int, db: Session = Depends(get_db)):
    stmt = select(Product).where(Product.id == product_id)
    product = db.scalars(stmt).first()
    if not product:
        raise HTTPException(status_code=404, detail="Product not found")
        
    db.delete(product)
    db.commit()
    return None
```

### One-to-Many Relationships (Authors & Books Example)

```python
from typing import List, Optional
from pydantic import BaseModel, ConfigDict
from sqlalchemy import Integer, String, ForeignKey
from sqlalchemy.orm import DeclarativeBase, Mapped, mapped_column, relationship

class Base(DeclarativeBase):
    pass

# SQLAlchemy Models
class AuthorDB(Base):
    __tablename__ = "authors"
    id: Mapped[int] = mapped_column(Integer, primary_key=True)
    name: Mapped[str] = mapped_column(String(50), nullable=False)
    books: Mapped[list["BookDB"]] = relationship(back_populates="author", cascade="all, delete-orphan")

class BookDB(Base):
    __tablename__ = "books"
    id: Mapped[int] = mapped_column(Integer, primary_key=True)
    title: Mapped[str] = mapped_column(String(100), nullable=False)
    author_id: Mapped[int] = mapped_column(Integer, ForeignKey("authors.id"))
    author: Mapped[AuthorDB] = relationship(back_populates="books")

# Pydantic Response Schemas
class BookResponse(BaseModel):
    id: int
    title: str
    model_config = ConfigDict(from_attributes=True)

class AuthorResponse(BaseModel):
    id: int
    name: str
    books: List[BookResponse] = []
    model_config = ConfigDict(from_attributes=True)
```

---

## Chapter 25: SQL Databases with SQLModel

### What is SQLModel? Merging Pydantic and SQLAlchemy

Created by Sebastián Ramírez (the creator of FastAPI), **SQLModel** bridges the gap between SQLAlchemy database models and Pydantic validation schemas. Instead of declaring models twice (once in Pydantic, once in SQLAlchemy), you declare them **once**:

```bash
pip install sqlmodel
```

### Creating Table Models and Pydantic Schemas in One Class

```python
from typing import Optional
from sqlmodel import SQLModel, Field

# Both an ORM Database Table AND a Pydantic Validation Schema!
class Hero(SQLModel, table=True):
    id: Optional[int] = Field(default=None, primary_key=True)
    name: str = Field(index=True)
    secret_name: str
    age: Optional[int] = Field(default=None, index=True)
```

### CRUD Operations with SQLModel and FastAPI

```python
from typing import List
from fastapi import FastAPI, Depends, HTTPException, status
from sqlmodel import SQLModel, create_engine, Session, select
from models import Hero

sqlite_url = "sqlite:///./heroes.db"
engine = create_engine(sqlite_url, connect_args={"check_same_thread": False})

def create_db_and_tables():
    SQLModel.metadata.create_all(engine)

def get_session():
    with Session(engine) as session:
        yield session

app = FastAPI()

@app.on_event("startup")
def on_startup():
    create_db_and_tables()

@app.post("/heroes/", response_model=Hero, status_code=status.HTTP_201_CREATED)
def create_hero(hero: Hero, session: Session = Depends(get_session)):
    session.add(hero)
    session.commit()
    session.refresh(hero)
    return hero

@app.get("/heroes/", response_model=List[Hero])
def read_heroes(session: Session = Depends(get_session)):
    heroes = session.exec(select(Hero)).all()
    return heroes
```

---

## Chapter 26: Database Migrations using Alembic

### Why Database Migrations are Mandatory

`create_all` creates missing tables, but will **never** alter existing tables or columns. When changing column definitions in live environments, **Alembic** manages forward and backward schema evolution.

### Initializing Alembic & Configuring env.py

```bash
pip install alembic
alembic init alembic
```

In `alembic/env.py`, connect your Declarative Base metadata:

```python
# In alembic/env.py
from database import Base
import models  # Ensures models are registered on Base

target_metadata = Base.metadata
```

### Autogenerating, Upgrading, and Rolling Back Migrations

```bash
# 1. Autogenerate migration script based on Python model changes
alembic revision --autogenerate -m "create users and products"

# 2. Upgrade database to the newest migration
alembic upgrade head

# 3. Rollback the last migration
alembic downgrade -1
```

### Folder Layout for Database Migrations

```text
my_project/
├── alembic.ini             # Alembic connection strings & settings
├── alembic/
│   ├── env.py              # Main execution environment script
│   ├── script.py.mako      # Migration file template
│   └── versions/           # Generated migration history
│       ├── 1a2b3c4d_initial_tables.py
│       ├── 2e3f4g5h_add_phone_to_users.py
│       └── 3i4j5k6l_add_discount_to_products.py
└── app/
    └── models.py
```

---

# Module 6: Security, Testing & Production Deployment

---

## Chapter 27: Password Hashing (Bcrypt) & Security Fundamentals

### Why Plaintext Passwords Mean Catastrophe

Databases can be leaked. Storing plaintext passwords compromises user accounts across every service where they reused credentials. A cryptographic password hash is an irreversible one-way digest:

$$\text{Password} + \text{Salt} \xrightarrow{\text{Bcrypt (12 Rounds)}} \$2b\$12\$e8...hashed\_output$$

### One-Way Cryptographic Hashing with Passlib & Bcrypt

```bash
pip install "passlib[bcrypt]"
```

```python
# security.py
from passlib.context import CryptContext

pwd_context = CryptContext(schemes=["bcrypt"], deprecated="auto")

def hash_password(password: str) -> str:
    """Produces secure salted one-way hash."""
    return pwd_context.hash(password)

def verify_password(plain_password: str, hashed_password: str) -> bool:
    """Verifies plaintext against stored hash digest."""
    return pwd_context.verify(plain_password, hashed_password)

if __name__ == '__main__':
    stored_hash = hash_password("SuperSecret2026!")
    print("Hash:", stored_hash)
    assert verify_password("SuperSecret2026!", stored_hash) is True
    assert verify_password("WrongPassword", stored_hash) is False
    print("Security checks passed.")
```

---

## Chapter 28: OAuth2, JWT Tokens, and User Authentication

### OAuth2 Password Flow & JWT Token Anatomy

A JWT (JSON Web Token) consists of three base64-encoded segments:
1. **Header:** Algorithm (`HS256`).
2. **Payload:** Claims (`sub` username, `exp` expiration).
3. **Signature:** Cryptographic verification signature preventing tampering.

```mermaid
sequenceDiagram
    autonumber
    actor Client
    participant API as FastAPI (/token)
    participant Protected as Protected Route (/users/me)

    Client->>API: POST /token (form-data: username="alice", password="password123")
    API->>API: Verify password hash
    API->>API: Generate signed JWT (exp, sub, role)
    API-->>Client: 200 OK {"access_token": "eyJhbGciOi...", "token_type": "bearer"}

    Note over Client: Client stores access_token in memory

    Client->>Protected: GET /users/me (Header: "Authorization: Bearer eyJhbGciOi...")
    Protected->>Protected: Verify JWT signature & expiration timestamp
    Protected-->>Client: 200 OK {"user": {"username": "alice", "role": "admin"}}
```

### Complete Working OAuth2 + JWT Implementation

```bash
pip install "pyjwt"
```

```python
import jwt
from datetime import datetime, timedelta
from typing import Optional
from fastapi import FastAPI, Depends, HTTPException, status
from fastapi.security import OAuth2PasswordBearer, OAuth2PasswordRequestForm
from pydantic import BaseModel

SECRET_KEY = "SUPER_SECRET_PRODUCTION_KEY_DO_NOT_HARDCODE"
ALGORITHM = "HS256"
ACCESS_TOKEN_EXPIRE_MINUTES = 30

oauth2_scheme = OAuth2PasswordBearer(tokenUrl="/token")

app = FastAPI()

class Token(BaseModel):
    access_token: str
    token_type: str

def create_access_token(data: dict, expires_delta: Optional[timedelta] = None) -> str:
    to_encode = data.copy()
    expire = datetime.utcnow() + (expires_delta or timedelta(minutes=15))
    to_encode.update({"exp": expire})
    return jwt.encode(to_encode, SECRET_KEY, algorithm=ALGORITHM)

# 1. Login Endpoint
@app.post("/token", response_model=Token)
def login(form_data: OAuth2PasswordRequestForm = Depends()):
    # Mock authentication check
    if form_data.username != "alice" or form_data.password != "secret123":
        raise HTTPException(
            status_code=status.HTTP_401_UNAUTHORIZED,
            detail="Incorrect username or password",
            headers={"WWW-Authenticate": "Bearer"},
        )
    
    token = create_access_token(
        data={"sub": form_data.username, "role": "admin"},
        expires_delta=timedelta(minutes=ACCESS_TOKEN_EXPIRE_MINUTES)
    )
    return {"access_token": token, "token_type": "bearer"}

# 2. Guard Dependency
def get_current_user(token: str = Depends(oauth2_scheme)):
    exception = HTTPException(
        status_code=status.HTTP_401_UNAUTHORIZED,
        detail="Could not validate credentials",
        headers={"WWW-Authenticate": "Bearer"},
    )
    try:
        payload = jwt.decode(token, SECRET_KEY, algorithms=[ALGORITHM])
        username: str = payload.get("sub")
        if username is None:
            raise exception
        return {"username": username, "role": payload.get("role")}
    except jwt.PyJWTError:
        raise exception

# 3. Protected Endpoint
@app.get("/users/me")
def read_current_user(current_user: dict = Depends(get_current_user)):
    return {"user": current_user}
```

---

## Chapter 29: Role-Based Access Control (RBAC) & Protected Routes

### Role Checking Dependency Factories

```python
from fastapi import FastAPI, Depends, HTTPException, status
# Reuses get_current_user from Chapter 28

app = FastAPI()

class RoleChecker:
    def __init__(self, allowed_roles: list[str]):
        self.allowed_roles = allowed_roles

    def __call__(self, user: dict = Depends(get_current_user)):
        user_role = user.get("role")
        if user_role not in self.allowed_roles:
            raise HTTPException(
                status_code=status.HTTP_403_FORBIDDEN,
                detail=f"Operation not permitted. Required roles: {self.allowed_roles}"
            )
        return user

allow_admin = RoleChecker(["admin"])
allow_staff = RoleChecker(["admin", "manager"])

@app.get("/admin/metrics", dependencies=[Depends(allow_admin)])
def view_system_metrics():
    return {"cpu_utilization": "14%", "active_workers": 8}
```

---

## Chapter 30: Asynchronous Programming in Python (async def vs def)

### How FastAPI Routes async def vs normal def

FastAPI's scheduler handles function definitions differently:

```
+-------------------+-----------------------------------+-----------------------------------+
| Signature         | Where FastAPI Executes It         | When You MUST Use It              |
+-------------------+-----------------------------------+-----------------------------------+
| async def         | Directly on ASGI Event Loop       | True async I/O (httpx, asyncpg)   |
| def (normal)      | External Thread Pool (anyio)      | Blocking calls (time.sleep,       |
|                   |                                   | standard requests, standard ORMs) |
+-------------------+-----------------------------------+-----------------------------------+
```

### The Danger of Blocking Synchronous Calls on the Event Loop

```python
import asyncio
import time
from fastapi import FastAPI

app = FastAPI()

# ✅ CORRECT: Non-blocking async sleep on event loop
@app.get("/async-correct")
async def async_correct():
    await asyncio.sleep(1.0)
    return {"message": "Non-blocking sleep completed"}

# ❌ FATAL ERROR: Blocking sleep stalls the ENTIRE server event loop!
@app.get("/async-danger")
async def async_danger():
    time.sleep(5.0)  # Freezes all other connected users for 5 seconds!
    return {"message": "Server stalled!"}

# ✅ CORRECT: Synchronous blocking code in standard def runs safely in worker threadpool
@app.get("/sync-safe")
def sync_safe():
    time.sleep(5.0)  # FastAPI runs this in a threadpool without stalling event loop
    return {"message": "Threadpool handled blocking task safely"}
```

---

## Chapter 31: Real-time Communication with WebSockets and Streaming

### WebSockets vs HTTP Polling

- **HTTP:** Request $\rightarrow$ Response $\rightarrow$ Closed socket. High latency for real-time dashboards.
- **WebSocket:** Persistent, bi-directional TCP connection. Low-overhead real-time messages.

### Multi-Client Broadcast WebSocket Manager

```python
from typing import List
from fastapi import FastAPI, WebSocket, WebSocketDisconnect

app = FastAPI()

class ConnectionManager:
    def __init__(self):
        self.active_connections: List[WebSocket] = []

    async def connect(self, websocket: WebSocket):
        await websocket.accept()
        self.active_connections.append(websocket)

    def disconnect(self, websocket: WebSocket):
        self.active_connections.remove(websocket)

    async def broadcast(self, message: str):
        for connection in self.active_connections:
            await connection.send_text(message)

manager = ConnectionManager()

@app.websocket("/ws/chat/{client_id}")
async def websocket_chat_endpoint(websocket: WebSocket, client_id: str):
    await manager.connect(websocket)
    await manager.broadcast(f"System: Client #{client_id} entered the room.")
    try:
        while True:
            data = await websocket.receive_text()
            await manager.broadcast(f"Client #{client_id}: {data}")
    except WebSocketDisconnect:
        manager.disconnect(websocket)
        await manager.broadcast(f"System: Client #{client_id} disconnected.")
```

### StreamingResponse & Server-Sent Events (SSE)

```python
import asyncio
from fastapi import FastAPI
from fastapi.responses import StreamingResponse

app = FastAPI()

async def stock_price_stream():
    for price in [100.1, 100.4, 101.2, 100.9, 102.0]:
        yield f"data: Current Price: ${price}\n\n"
        await asyncio.sleep(1.0)

@app.get("/prices")
def stream_prices():
    return StreamingResponse(stock_price_stream(), media_type="text/event-stream")
```

---

## Chapter 32: Automated Testing with pytest and TestClient

### FastAPI TestClient with httpx

```bash
pip install pytest httpx
```

### In-Memory Test Database Fixtures & Dependency Overrides

```python
# test_app.py
from fastapi.testclient import TestClient
from sqlalchemy import create_engine
from sqlalchemy.orm import sessionmaker

from main import app
from database import Base, get_db

# 1. In-memory SQLite engine
TEST_DB_URL = "sqlite:///:memory:"
test_engine = create_engine(TEST_DB_URL, connect_args={"check_same_thread": False})
TestingSessionLocal = sessionmaker(autocommit=False, autoflush=False, bind=test_engine)

Base.metadata.create_all(bind=test_engine)

# 2. Dependency override
def override_get_db():
    db = TestingSessionLocal()
    try:
        yield db
    finally:
        db.close()

app.dependency_overrides[get_db] = override_get_db
client = TestClient(app)
```

### Writing Comprehensive Test Cases with Expected Assertions

```python
def test_create_product_success():
    payload = {"title": "Desk Lamp", "price": 24.99}
    response = client.post("/products/", json=payload)
    assert response.status_code == 201
    data = response.json()
    assert data["title"] == "Desk Lamp"
    assert data["price"] == 24.99
    assert "id" in data

def test_create_product_validation_error():
    # Price must be positive; sending negative should fail with 422
    payload = {"title": "Broken Item", "price": -10.0}
    response = client.post("/products/", json=payload)
    assert response.status_code == 422
    errors = response.json()["detail"]
    assert any(err["loc"][-1] == "price" for err in errors)

def test_get_nonexistent_product_404():
    response = client.get("/products/999999")
    assert response.status_code == 404
    assert response.json()["detail"] == "Product not found"
```

Run test suite:
```bash
pytest -v
```

**Expected pytest Output:**
```text
============================= test session starts ==============================
collected 3 items

tests/test_products.py::test_create_product_success PASSED               [ 33%]
tests/test_products.py::test_create_product_validation_error PASSED      [ 66%]
tests/test_products.py::test_get_nonexistent_product_404 PASSED          [100%]

============================== 3 passed in 0.42s ===============================
```

---

## Chapter 33: Containerization with Docker & Production Deployment

### Production Multi-Stage Dockerfile

```dockerfile
# Stage 1: Build stage
FROM python:3.11-slim as builder

WORKDIR /app

ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1

RUN apt-get update && apt-get install -y --no-install-recommends gcc libpq-dev && rm -rf /var/lib/apt/lists/*

COPY requirements.txt .
RUN pip install --user --no-cache-dir -r requirements.txt

# Stage 2: Final runtime image
FROM python:3.11-slim

WORKDIR /app

RUN groupadd -r appgroup && useradd -r -g appgroup appuser

COPY --from=builder /root/.local /home/appuser/.local
COPY . /app

ENV PATH=/home/appuser/.local/bin:$PATH

USER appuser

EXPOSE 8000

CMD ["gunicorn", "-w", "4", "-k", "uvicorn.workers.UvicornWorker", "main:app", "--bind", "0.0.0.0:8000"]
```

### docker-compose.yml for FastAPI & PostgreSQL

```yaml
version: "3.8"

services:
  web:
    build: .
    container_name: fastapi_api_server
    restart: always
    ports:
      - "8000:8000"
    environment:
      - DATABASE_URL=postgresql://postgres:secretpassword@db:5432/production_db
      - SECRET_KEY=production_secret_key_here
    depends_on:
      - db

  db:
    image: postgres:15-alpine
    container_name: postgres_database
    restart: always
    environment:
      - POSTGRES_USER=postgres
      - POSTGRES_PASSWORD=secretpassword
      - POSTGRES_DB=production_db
    volumes:
      - postgres_data:/var/lib/postgresql/data
    ports:
      - "5432:5432"

volumes:
  postgres_data:
```

### Nginx Reverse Proxy Configuration (nginx.conf)

```nginx
# nginx/nginx.conf
events { worker_connections 1024; }

http {
    upstream fastapi_app {
        server web:8000;
    }

    server {
        listen 80;
        server_name api.example.com;

        location / {
            proxy_pass http://fastapi_app;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header X-Forwarded-Proto $scheme;
        }

        # WebSocket support
        location /ws/ {
            proxy_pass http://fastapi_app;
            proxy_http_version 1.1;
            proxy_set_header Upgrade $http_upgrade;
            proxy_set_header Connection "upgrade";
            proxy_set_header Host $host;
        }
    }
}
```

### Production Architecture: Nginx + Gunicorn (Uvicorn Workers)

```mermaid
flowchart TD
    Client["Clients (Web / iOS / Android)"] -->|"HTTPS: 443"| Nginx["Nginx Reverse Proxy (SSL Termination, Rate Limiting)"]
    Nginx -->|"Proxy Pass: 8000"| Gunicorn["Gunicorn Master Process"]
    
    subgraph Workers["Uvicorn Worker Pool"]
        W1["Uvicorn Worker 1 (FastAPI ASGI)"]
        W2["Uvicorn Worker 2 (FastAPI ASGI)"]
        W3["Uvicorn Worker 3 (FastAPI ASGI)"]
        W4["Uvicorn Worker 4 (FastAPI ASGI)"]
    end
    
    Gunicorn --> W1
    Gunicorn --> W2
    Gunicorn --> W3
    Gunicorn --> W4
    
    W1 -->|"SQLAlchemy Pool"| DB[("PostgreSQL Database: 5432")]
    W2 --> DB
    W3 --> DB
    W4 --> DB
```

---

## Master Quick-Reference Summary

| Topic | Primary Tool | Key Function / Class |
| :--- | :--- | :--- |
| **Routing** | FastAPI | `@app.get()`, `@app.post()`, `APIRouter` |
| **Path Constraints** | FastAPI | `Path(..., ge=1, le=100)` |
| **Query Constraints** | FastAPI | `Query(None, min_length=3, pattern=r"...")` |
| **Data Validation** | Pydantic V2 | `BaseModel`, `Field`, `@field_validator` |
| **Multi-Parameter Body**| FastAPI | `Body(..., embed=True)` |
| **Header / Cookie** | FastAPI | `Header()`, `Cookie()`, Header/Cookie Models |
| **Dependency Injection**| FastAPI | `Depends()`, `yield` generator lifecycles |
| **Database ORM** | SQLAlchemy 2.0 / SQLModel | `Mapped`, `mapped_column`, `SQLModel` |
| **Migrations** | Alembic | `alembic revision --autogenerate`, `alembic upgrade head` |
| **Password Security** | Passlib | `CryptContext(schemes=["bcrypt"])` |
| **Authentication** | PyJWT & OAuth2 | `OAuth2PasswordBearer`, `jwt.encode()`, `jwt.decode()` |
| **Asynchronous Engine**| Starlette / AnyIO | `async def` (Event loop) vs `def` (Thread pool) |
| **Real-time Comms** | WebSockets | `@app.websocket()`, `WebSocketDisconnect` |
| **Testing** | Pytest & TestClient | `client.post()`, `app.dependency_overrides` |
| **Production Hosting** | Gunicorn + Uvicorn | `gunicorn -k uvicorn.workers.UvicornWorker` |
