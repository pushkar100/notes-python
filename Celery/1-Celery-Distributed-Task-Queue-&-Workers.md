# The Definitive Celery Tutorial: From Zero to Production

A friendly, step-by-step guide to distributed background tasks in Python using Celery, RabbitMQ, Redis, Flask, FastAPI, and Django.

## Table of Contents

1. [Quickstart: The Complete 3-Minute Working Example (Code First!)](#1-quickstart-the-complete-3-minute-working-example-code-first)
2. [The Problem Celery Solves (Why Do We Need It?)](#2-the-problem-celery-solves-why-do-we-need-it)
3. [Core Architecture Explained in Plain English](#3-core-architecture-explained-in-plain-english)
4. [Celery's Core Methods & Concepts Explained](#4-celerys-core-methods--concepts-explained)
5. [Essential Rules Every Beginner Must Know](#5-essential-rules-every-beginner-must-know)
6. [Hands-On Beginner Labs (Do-It-Yourself Code)](#6-hands-on-beginner-labs-do-it-yourself-code)
7. [Beginner-Friendly Web Framework Integrations (Flask, FastAPI, Django)](#7-beginner-friendly-web-framework-integrations-flask-fastapi-django)
8. [Scaling Workers: From Local Machine to Real-World Production](#8-scaling-workers-from-local-machine-to-real-world-production)
9. [Production Best Practices & Monitoring](#9-production-best-practices--monitoring)

---

## 1. Quickstart: The Complete 3-Minute Working Example (Code First!)

Before diving into theory, let's run a complete, working Celery system on your machine. You will see tasks get sent, queued, executed by a background worker, and the final answer collected.

### The Restaurant Analogy

Think of Celery like a busy pizza restaurant:

- **Client (You / Web App):** The cashier taking the order.
- **Message Broker (Redis/RabbitMQ):** The order slip rack where new pizza orders hang.
- **Worker (Celery Worker):** The pizza chef in the kitchen baking the pizza.
- **Result Backend (Redis):** The pickup counter where finished pizzas sit with order numbers.

The cashier does NOT bake the pizza. They take the order, give you an order ticket, and immediately welcome the next customer!

### Visual Sequence of Events

```mermaid
sequenceDiagram
    autonumber
    actor User
    participant Client as Client (client.py)
    participant Broker as Broker (Redis DB 0)
    participant Worker as Worker (tasks.py)
    participant Backend as Backend (Redis DB 1)

    User->>Client: Run script
    Client->>Broker: .delay(25, 75) [Pushes task message to queue]
    Broker-->>Client: Returns Task ID immediately
    Client->>Client: Continues running (does not freeze!)
    Worker->>Broker: Pulls task from queue
    Worker->>Backend: Updates status = STARTED
    Worker->>Worker: Executes add_numbers(25, 75)
    Worker->>Backend: Stores result (100) & status = SUCCESS
    loop Polls every 1 second
        Client->>Backend: Is task ready?
        Backend-->>Client: Not ready... / Yes, result is 100!
    end
    Client->>User: Displays final result: 100
```

### The Three Files You Need

Create a new folder and add these 3 files:

### File 1: `docker-compose.yml` (Starts Redis)

Redis will act as both our Message Broker (the order rack) and Result Backend (the pickup counter).

```yaml
services:
  redis:
    image: redis:7-alpine
    container_name: celery-redis
    ports:
      - "6379:6379"
```

### File 2: `tasks.py` (Defines the Task & Worker Setup)

This file defines what work our chef (worker) knows how to do.

```python
# tasks.py
import time
from celery import Celery

# Step 1: Create the Celery app
# 'quickstart' is the name of this project
# broker: Where task messages wait in line (Redis database 0)
# backend: Where finished return values are stored (Redis database 1)
app = Celery(
    'quickstart',
    broker='redis://localhost:6379/0',
    backend='redis://localhost:6379/1'
)

# Optional settings
app.conf.update(
    task_track_started=True,  # Tell us when a worker has started working on a task
    result_expires=3600,       # Delete finished results after 1 hour (cleans up memory)
)

# Step 2: Define a background task using the @app.task decorator
@app.task
def add_numbers(x, y):
    print(f"--> [Worker] Received: {x} + {y}. Starting work...")
    time.sleep(4)  # Simulate 4 seconds of heavy work
    answer = x + y
    print(f"--> [Worker] Finished work! Result: {answer}")
    return answer
```

### File 3: `client.py` (Sends the Task & Checks the Result)

This file acts like our user or web application asking for work to be done.

```python
# client.py
import time
from tasks import add_numbers

if __name__ == '__main__':
    print("1. [Client] Sending task to Celery...")

    # .delay() is the magic command!
    # It packs up (25, 75) into a message, sends it to Redis, and returns INSTANTLY!
    async_result = add_numbers.delay(25, 75)

    print(f"2. [Client] Task sent! Ticket / Task ID: {async_result.id}")
    print("3. [Client] Notice: our script did NOT freeze for 4 seconds!")

    # Now let's poll the result backend to see when the worker is done
    print("\n4. [Client] Checking if worker is done...")
    while not async_result.ready():  # Note: ready() is a function call with parentheses ()!
        print(f"   Current status: {async_result.state} (Waiting for worker...)")
        time.sleep(1)

    print("\n5. [Client] Worker finished!")
    print(f"   Final Status: {async_result.state}")
    print(f"   Final Result: {async_result.get()}")
```

### Running It in 3 Terminals

First, install Celery and Redis in your Python environment:

```bash
pip install celery redis
```

#### Terminal 1: Start Redis

```bash
docker compose up
```

_(Redis is now running on port 6379)_

#### Terminal 2: Start the Celery Worker

In the same folder as `tasks.py`, run:

```bash
celery -A tasks worker --loglevel=info
```

You will see the Celery banner appear, showing `Connected to redis://localhost:6379/0` and `ready`.

#### Terminal 3: Run the Client Script

```bash
python client.py
```

### Visual Output: What You See Happening

```text
TERMINAL 3: python client.py                 TERMINAL 2: celery worker
=======================================      =================================================
1. [Client] Sending task to Celery...
2. [Client] Task sent! Task ID: 8a71-...
3. [Client] Notice: script did NOT freeze!
4. [Client] Checking if worker is done...
   Current status: PENDING
                                             [Received task: tasks.add_numbers[8a71-...]]
                                             --> [Worker] Received: 25 + 75. Starting work...
   Current status: STARTED
   Current status: STARTED
   Current status: STARTED
                                             --> [Worker] Finished work! Result: 100
                                             [Task tasks.add_numbers[8a71-...] succeeded in 4.01s: 100]
5. [Client] Worker finished!
   Final Status: SUCCESS
   Final Result: 100
```

---

## 2. The Problem Celery Solves (Why Do We Need It?)

### Synchronous vs. Asynchronous: What Does "Blocking" Mean?

In normal Python code, lines run one after another:

```python
send_welcome_email(user)   # Takes 3 seconds
create_user_profile(user)  # Waits 3 seconds before this can start!
```

This is **synchronous (blocking)**. Each line freezes everything until it finishes.

### The Web Server Dilemma

```text
SYNCHRONOUS ARCHITECTURE (POOR USER EXPERIENCE):
[User Browser] === POST /generate-report ===> [Web Server Worker]
                                                    |
                                            (Generating PDF...)
                                            (Takes 25 seconds!)
                                            (Server worker is frozen!)
                                                    |
[User Browser] <=== Waits 25s or TIMEOUT (504) =====+


ASYNCHRONOUS ARCHITECTURE WITH CELERY (BLAZING FAST):
[User Browser] === POST /generate-report ===> [Web Server Worker]
                                                    |
                                            1. Push task to Queue (0.001s)
                                            2. Return Task ID: #8a71
                                                    |
[User Browser] <=== HTTP 202 Accepted (0.01s) ======+
                                                    |
                                                    v (In background)
                                            [Celery Worker]
                                            Generates PDF safely
```

During those 25 seconds in the synchronous model:

1. The user stares at a spinning loading wheel, thinking your site is broken.
2. The web server process is completely busy and cannot serve other visitors.
3. If 20 people click "Generate Report" at once, all web workers freeze and your site crashes with `504 Gateway Timeout`.

With Celery, the web server offloads the job in 2 milliseconds, frees itself up for other users, and lets the Celery worker do the heavy lifting in the background.

---

## 3. Core Architecture Explained in Plain English

Celery is composed of 4 main pieces working together:

```mermaid
flowchart LR
    subgraph Producers ["1. The Clients (Producers)"]
        Web["Web Server (Flask/FastAPI/Django)"]
        CLI["Script or CLI"]
    end

    subgraph Broker ["2. Message Broker (The Queue)"]
        Queue[("RabbitMQ / Redis\nTask Queue")]
    end

    subgraph Workers ["3. Celery Workers (Consumers)"]
        W1["Worker Node 1\n(Executes Task)"]
        W2["Worker Node 2\n(Executes Task)"]
    end

    subgraph Backend ["4. Result Backend (Storage)"]
        DB[("Redis / Database\nReturn Values & States")]
    end

    Web -->|1. .delay()| Queue
    CLI -->|1. .delay()| Queue
    Queue -->|2. Prefetch| W1
    Queue -->|2. Prefetch| W2
    W1 -->|3. Save Result| DB
    W2 -->|3. Save Result| DB
    Web -.->|4. Check Status| DB
```

### The 4 Main Actors

1. **The Client (Producer):**
   Your normal application code (Flask route, FastAPI endpoint, or CLI script). It never runs the task itself. It simply writes an instruction note and drops it in the broker.
2. **The Message Broker (The Post Office):**
   The queue holding the task notes. If 10,000 tasks are requested at once, the broker lines them up safely in memory or on disk so nothing gets lost.
3. **The Celery Worker (The Chef):**
   A separate Python program running in your terminal or a Docker container. It watches the broker, grabs the next task note, executes the Python function, and handles errors.
4. **The Result Backend (The Filing Cabinet):**
   A storage place where the worker files away the return value (e.g. `100`) or error message so the client can read it later.

### RabbitMQ vs. Redis: Which One Should You Use?

| Feature           | Redis                                                             | RabbitMQ                                                      |
| :---------------- | :---------------------------------------------------------------- | :------------------------------------------------------------ |
| **What is it?**   | Superfast in-memory cache/database                                | Dedicated enterprise message broker                           |
| **Ease of Setup** | Extremely easy; lightweight                                       | Moderate; slightly heavier                                    |
| **Data Safety**   | Stores in RAM by default. A sudden crash could lose queued tasks. | Very safe. Writes messages to disk; guarantees task delivery. |
| **Best Used As**  | Great for Development and as a **Result Backend**                 | The industry standard for **Message Broker** in production    |

**Beginner Recommendation:**

- For learning and small projects: Use **Redis** for both Broker and Backend.
- For production enterprise apps: Use **RabbitMQ** as the Broker and **Redis** as the Result Backend.

### Multi-Container Docker Setup (RabbitMQ + Redis + Worker)

Here is a full `docker-compose.yml` combining both:

```yaml
services:
  rabbitmq:
    image: rabbitmq:3-management
    environment:
      RABBITMQ_DEFAULT_USER: user
      RABBITMQ_DEFAULT_PASS: password
    ports:
      - "5672:5672" # Broker connection
      - "15672:15672" # Web dashboard to view queues
    volumes:
      - rabbitmq_data:/var/lib/rabbitmq
    healthcheck:
      test: ["CMD-SHELL", "rabbitmq-diagnostics -q ping"]
      interval: 10s
      timeout: 5s
      retries: 5

  redis:
    image: redis:7-alpine
    ports:
      - "6379:6379"
    volumes:
      - redis_data:/data
    healthcheck:
      test: ["CMD-SHELL", "redis-cli ping | grep PONG"]
      interval: 10s
      timeout: 5s
      retries: 5

  celery_worker:
    build: .
    command: celery -A tasks worker --loglevel=info
    environment:
      CELERY_BROKER_URL: amqp://user:password@rabbitmq:5672//
      CELERY_BACKEND_URL: redis://redis:6379/0
    depends_on:
      rabbitmq:
        condition: service_healthy
      redis:
        condition: service_healthy

volumes:
  rabbitmq_data:
  redis_data:
```

### Worker Concurrency & Execution Pools

When you launch a worker, how does it run multiple tasks at once?
Celery gives you execution pools via the `-P` flag:

- **`prefork` (Default):** Spawns separate CPU processes. Best for math, data processing, and image resizing.
  `celery -A tasks worker --concurrency=4` (runs 4 tasks simultaneously).
- **`threads`:** Uses lightweight threads. Best for network requests.
  `celery -A tasks worker -P threads -c 10`
- **`solo`:** Runs everything in a single plain process. Great for beginners debugging with `print()` or `pdb`.
  `celery -A tasks worker -P solo`

---

## 4. Celery's Core Methods & Concepts Explained

Let's demystify every important method you will see in Celery code.

### 1. Task Dispatching Methods

#### `task.delay(*args, **kwargs)`

- **Concept:** "Do this as soon as possible in the background."
- **Usage:**
  ```python
  # Calls add_numbers(10, 20) in the background
  result = add_numbers.delay(10, 20)
  ```
- **What it returns:** An `AsyncResult` object.

#### `task.apply_async(args=(), kwargs={}, ...options)`

- **Concept:** "Do this in the background, but with special instructions" (e.g. wait 30 seconds, send to a specific queue, or expire if delayed).
- **Usage:**

  ```python
  # Example A: Wait 60 seconds before executing (countdown)
  send_reminder.apply_async(args=[user_id], countdown=60)

  # Example B: Run at a specific date and time (ETA)
  import datetime
  tomorrow = datetime.datetime.now(datetime.timezone.utc) + datetime.timedelta(days=1)
  send_reminder.apply_async(args=[user_id], eta=tomorrow)

  # Example C: Send to a high-priority queue
  process_payment.apply_async(args=[order_id], queue='urgent')

  # Example D: Expire if not started within 120 seconds
  generate_otp.apply_async(args=[phone], expires=120)
  ```

#### `task.s(*args)` (Signatures)

- **Concept:** A "recipe" or "blueprint" of a task call that you can pass around or combine into pipelines before executing it.
- **Usage:**

  ```python
  # Creates a signature without running it yet
  recipe = add_numbers.s(10, 20)

  # Run it later whenever you want
  result = recipe.delay()
  ```

### 2. Result Inspection Methods (`AsyncResult`)

When you run `res = my_task.delay()`, `res` is an `AsyncResult`.

```mermaid
stateDiagram-v2
    [*] --> PENDING: Task Dispatched
    PENDING --> STARTED: Worker picks up task
    STARTED --> SUCCESS: Function finishes without error
    STARTED --> FAILURE: Unhandled Exception
    STARTED --> RETRY: Handled Exception & retry requested
    RETRY --> PENDING: Waits countdown, re-enters queue
    PENDING --> REVOKED: Canceled before running
    STARTED --> REVOKED: Terminated while running
    SUCCESS --> [*]
    FAILURE --> [*]
    REVOKED --> [*]
```

Here are its essential inspection methods:

#### `result.ready()`

- **Concept:** "Is the task completely finished?"
- **Returns:** `True` if completed (whether successful or failed), `False` if still waiting or running.
- **Common Beginner Trap:**

  ```python
  # BAD: ready is a method, forgetting () makes it always True!
  if result.ready:    # BUG!
      print("Done!")

  # GOOD:
  if result.ready():  # CORRECT!
      print("Done!")
  ```

#### `result.get(timeout=None)`

- **Concept:** "Wait and give me the return value."
- **Behavior:** This is **blocking**! If the task takes 5 seconds, `result.get()` will pause your current script for 5 seconds until the answer is ready.
  ```python
  # Block for up to 10 seconds. If it takes longer, raise TimeoutError
  try:
      val = result.get(timeout=10)
      print("Got value:", val)
  except TimeoutError:
      print("Task took too long!")
  ```

#### `result.state` (or `result.status`)

- **Concept:** The current lifecycle label of the task (`PENDING`, `STARTED`, `SUCCESS`, `FAILURE`, `RETRY`, `REVOKED`).

#### `result.successful()` and `result.failed()`

- Boolean checks:
  ```python
  if result.successful():
      print("Task succeeded with:", result.result)
  elif result.failed():
      print("Task failed with error:", result.result)
  ```

#### `result.forget()`

- Deletes the task result from Redis to free up memory.

### 3. Inside-the-Worker Methods (`bind=True`)

When defining a task, you can add `bind=True`. This passes `self` (the task itself) as the first argument, unlocking powerful controls:

```python
@app.task(bind=True)
def my_worker_task(self, filename):
    # 1. Inspect task metadata
    print("My unique Task ID is:", self.request.id)
    print("Current retry attempt:", self.request.retries)

    # 2. Update live progress
    self.update_state(state='PROGRESS', meta={'percent': 50})

    # 3. Retry on failure
    try:
        download_file(filename)
    except ConnectionError as exc:
        raise self.retry(exc=exc, countdown=10)
```

---

## 5. Essential Rules Every Beginner Must Know

### Rule 1: Never Pass Complex Objects into Tasks!

Celery converts all arguments to **JSON** text before sending them through the broker.

```python
# BAD! Passing a database object or open file
user = User.objects.get(id=42)
send_welcome.delay(user)  # CRASH! Database models cannot be converted to JSON.

# GOOD! Pass the simple integer ID:
send_welcome.delay(user_id=42)

# Inside the task, re-fetch the user:
@app.task
def send_welcome(user_id):
    user = User.objects.get(id=user_id)
    ...
```

### Rule 2: Tasks Must Be "Idempotent"

In a distributed network, a task might get executed more than once (e.g. if a worker crashes right as it finishes).
An **idempotent** task produces the same outcome whether run once or three times.

- **Non-idempotent:** `bank_account.balance -= 100` (Running twice charges $200!).
- **Idempotent:** `charge_order_with_unique_token(order_id, token="abc")` (Payment gateway detects duplicate token and ignores second charge).

### Rule 3: Disable Results If You Don't Need Them

If a task just sends an email or clears temporary files, you don't need to store a return value in Redis:

```python
@app.task(ignore_result=True)
def send_email(to, body):
    ...
```

This saves database connections and prevents Redis from running out of RAM.

---

## 6. Hands-On Beginner Labs (Do-It-Yourself Code)

### Lab 1: Live Progress Bar (0% to 100%)

How to let your users know how much work has completed.

Create `lab1_progress.py`:

```python
import time
from celery import Celery

app = Celery('progress_app', broker='redis://localhost:6379/0', backend='redis://localhost:6379/1')

@app.task(bind=True)
def process_batch(self, total_items):
    for i in range(1, total_items + 1):
        time.sleep(0.5)  # Simulate processing 1 item
        percent = int((i / total_items) * 100)

        # Report progress back to Redis
        self.update_state(
            state='PROGRESS',
            meta={'current': i, 'total': total_items, 'percent': percent}
        )
    return {'status': 'Completed all items!'}

if __name__ == '__main__':
    # Start task
    task = process_batch.delay(6)
    print(f"Task started: {task.id}")

    # Monitor progress
    while not task.ready():
        if task.state == 'PROGRESS':
            info = task.info  # contains the meta dictionary
            print(f"Progress: [{info.get('percent')}%] ({info.get('current')}/{info.get('total')})")
        time.sleep(0.5)

    print("Result:", task.get())
```

Run in 2 terminals:

- Worker: `celery -A lab1_progress.app worker --loglevel=info`
- Client: `python lab1_progress.py`

### Lab 2: Bulletproof Error Retries

Real-world networks fail. Celery can automatically retry with **exponential backoff** (waiting 1s, then 2s, then 4s...).

Create `lab2_retry.py`:

```python
import random
from celery import Celery

app = Celery('retry_app', broker='redis://localhost:6379/0', backend='redis://localhost:6379/1')

class ThirdPartyAPIError(Exception):
    """Custom error for flaky API"""
    pass

@app.task(
    autoretry_for=(ThirdPartyAPIError,),  # Automatically retry if this error happens
    retry_kwargs={'max_retries': 3},     # Try at most 3 times
    retry_backoff=2,                     # Wait 2s, then 4s, then 8s
)
def fetch_weather(city):
    print(f"Attempting to fetch weather for {city}...")
    # Simulate 60% chance of temporary network failure
    if random.random() < 0.6:
        print("  -> Connection dropped! Raising error...")
        raise ThirdPartyAPIError("Weather server did not respond")

    print("  -> Success!")
    return {"city": city, "temp": "22°C"}

if __name__ == '__main__':
    result = fetch_weather.delay("London")
    try:
        print("Final Output:", result.get(timeout=20))
    except Exception as e:
        print("Task failed permanently after 3 retries:", e)
```

Run in 2 terminals:

- Worker: `celery -A lab2_retry.app worker --loglevel=info`
- Client: `python lab2_retry.py`

### Lab 3: Celery Canvas (Pipelines & Workflows)

Celery provides 3 core primitives to connect tasks together:

```text
1. CHAIN (Sequential Pipeline):
   [step_one(5)] === Output 10 ===> [step_two()] === Output 20 ===> Result: 20

2. GROUP (Parallel Execution):
   +---> [step_one(1)] ---> 2  ---+
   +---> [step_one(2)] ---> 4  ---+---> Combined list: [2, 4, 6, 8]
   +---> [step_one(3)] ---> 6  ---+
   +---> [step_one(4)] ---> 8  ---+

3. CHORD (Parallel Map + Combine Callback):
   +---> [step_one(1)] ---> 2  ---+
   +---> [step_one(2)] ---> 4  ---+---> [sum_all([2, 4, 6, 8])] ===> Result: 20
   +---> [step_one(3)] ---> 6  ---+
   +---> [step_one(4)] ---> 8  ---+
```

Create `lab3_canvas.py`:

```python
import time
from celery import Celery, chain, group, chord

app = Celery('canvas_app', broker='redis://localhost:6379/0', backend='redis://localhost:6379/1')

@app.task
def step_one(x):
    return x * 2

@app.task
def step_two(x):
    return x + 10

@app.task
def sum_all(numbers):
    return sum(numbers)

if __name__ == '__main__':
    # 1. CHAIN: Run sequentially: (5 * 2) -> (10 + 10) = 20
    print("\n--- Testing Chain (Sequential) ---")
    pipeline = chain(step_one.s(5) | step_two.s())
    print("Chain Result:", pipeline().get())

    # 2. GROUP: Run 4 tasks at the exact same time in parallel
    print("\n--- Testing Group (Parallel) ---")
    parallel_jobs = group(step_one.s(i) for i in [1, 2, 3, 4])
    print("Group Results:", parallel_jobs().get())

    # 3. CHORD: Run group in parallel, then pass all results to a final callback
    print("\n--- Testing Chord (Map-Reduce) ---")
    my_chord = chord([step_one.s(i) for i in [1, 2, 3, 4]])(sum_all.s())
    print("Chord Final Sum Result:", my_chord.get())
```

### Lab 4: Periodic Tasks & Scheduling (Celery Beat)

Celery Beat is like a built-in `cron` job scheduler.
It runs as a clock: when a scheduled time arrives, it sends a task message to the worker.

```mermaid
flowchart TD
    Clock["Celery Beat (Clock Process)\nChecks schedule every tick"]
    Queue[("Message Broker\nQueue")]
    Worker1["Worker Node 1"]
    Worker2["Worker Node 2"]

    Clock -->|Every 5s: 'Run heartbeat'| Queue
    Clock -->|Every Midnight: 'Run backup'| Queue
    Queue --> Worker1
    Queue --> Worker2
```

Here are **4 clear examples**, from dead simple to daily cron:

Create `lab4_schedule.py`:

```python
from celery import Celery
from celery.schedules import crontab

app = Celery('scheduler_app', broker='redis://localhost:6379/0', backend='redis://localhost:6379/1')

# Define our scheduled tasks
@app.task
def simple_heartbeat():
    print(">>> [HEARTBEAT] Ping! System is alive.")
    return "ALIVE"

@app.task
def generate_hourly_metrics():
    print(">>> [HOURLY] Calculating traffic metrics for the past hour...")
    return "METRICS_SAVED"

@app.task
def midnight_backup():
    print(">>> [DAILY CRON] Running midnight database backup...")
    return "BACKUP_SUCCESS"

# Configure the schedules in the beat dictionary
app.conf.beat_schedule = {
    # Example 1: Super Simple - Run every 5 seconds
    'ping-every-5-seconds': {
        'task': 'lab4_schedule.simple_heartbeat',
        'schedule': 5.0,  # 5.0 seconds
    },

    # Example 2: Run every 30 minutes
    'calculate-metrics-every-30-mins': {
        'task': 'lab4_schedule.generate_hourly_metrics',
        'schedule': 1800.0,  # 1800 seconds = 30 minutes
    },

    # Example 3: Cron Schedule - Run every night at midnight (00:00 UTC)
    'backup-every-midnight': {
        'task': 'lab4_schedule.midnight_backup',
        'schedule': crontab(hour=0, minute=0),
    },

    # Example 4: Cron Schedule - Run every Monday at 8:30 AM
    'monday-morning-report': {
        'task': 'lab4_schedule.generate_hourly_metrics',
        'schedule': crontab(hour=8, minute=30, day_of_week=1),
    },
}
```

#### How to run Celery Beat:

You need **two** commands running:

1. **Terminal 1 (Worker that actually does the work):**
   ```bash
   celery -A lab4_schedule.app worker --loglevel=info
   ```
2. **Terminal 2 (Beat Scheduler that acts as the alarm clock):**
   ```bash
   celery -A lab4_schedule.app beat --loglevel=info
   ```
   Watch Terminal 2 trigger every 5 seconds and Terminal 1 execute the task!

### Lab 5: Task Routing & Dedicated Queues

Prevent slow tasks (video conversion) from delaying urgent tasks (password reset email).

```mermaid
flowchart LR
    subgraph TasksDispatched ["Tasks Dispatched"]
        T1["send_password_reset()"]
        T2["process_heavy_video()"]
    end

    subgraph Queues ["Dedicated Broker Queues"]
        Q1[("Queue: 'urgent'")]
        Q2[("Queue: 'low_priority'")]
    end

    subgraph Workers ["Specialized Workers"]
        W1["Urgent Worker (-Q urgent)\nFast & responsive"]
        W2["Heavy Worker (-Q low_priority)\nLong running jobs"]
    end

    T1 -->|Route: urgent| Q1
    T2 -->|Route: low_priority| Q2
    Q1 --> W1
    Q2 --> W2
```

Create `lab5_routing.py`:

```python
import time
from celery import Celery

app = Celery('routing_app', broker='redis://localhost:6379/0')

# Route tasks to specific named queues
app.conf.task_routes = {
    'lab5_routing.send_password_reset': {'queue': 'urgent'},
    'lab5_routing.process_heavy_video': {'queue': 'low_priority'},
}

@app.task
def send_password_reset(email):
    print(f"[URGENT QUEUE] Sending immediate password reset to {email}!")
    return "EMAIL_SENT"

@app.task
def process_heavy_video(video_id):
    print(f"[LOW PRIORITY QUEUE] Processing heavy video {video_id} (10 seconds)...")
    time.sleep(10)
    return "VIDEO_DONE"
```

#### Running Workers on Specific Queues:

You can start a worker dedicated **only** to urgent jobs:

```bash
# Dedicated urgent worker (always fast!)
celery -A lab5_routing.app worker -Q urgent --loglevel=info

# Background worker for everything else
celery -A lab5_routing.app worker -Q low_priority,celery --loglevel=info
```

---

## 7. Beginner-Friendly Web Framework Integrations (Flask, FastAPI, Django)

### 1. Complete Flask Example

In Flask, we use an application factory to make sure Celery tasks have access to Flask's configurations and database.

#### Directory Structure:

```text
flask_demo/
├── app.py
```

#### `app.py`:

```python
import time
from flask import Flask, jsonify, request
from celery import Celery, Task

def make_celery(flask_app: Flask) -> Celery:
    """Links Celery to Flask application context"""
    class FlaskTask(Task):
        def __call__(self, *args, **kwargs):
            with flask_app.app_context():
                return self.run(*args, **kwargs)

    celery_app = Celery(flask_app.import_name, task_cls=FlaskTask)
    celery_app.config_from_object(flask_app.config["CELERY"])
    celery_app.set_default()
    return celery_app

# 1. Create Flask app
app = Flask(__name__)
app.config.from_mapping(
    CELERY=dict(
        broker_url="redis://localhost:6379/0",
        result_backend="redis://localhost:6379/1",
    )
)

# 2. Initialize Celery
celery_app = make_celery(app)

# 3. Define Celery Task
@celery_app.task
def send_welcome_email(user_email):
    time.sleep(5)  # Simulate sending email
    return f"Email successfully sent to {user_email}"

# 4. Route 1: Trigger the task (Returns immediately!)
@app.route("/signup", methods=["POST"])
def signup():
    data = request.get_json() or {}
    email = data.get("email", "newuser@example.com")

    # Send to Celery
    task = send_welcome_email.delay(email)

    return jsonify({
        "message": "User registered! Sending email in background.",
        "task_id": task.id,
        "check_status_url": f"/status/{task.id}"
    }), 202

# 5. Route 2: Poll status
@app.route("/status/<task_id>", methods=["GET"])
def check_status(task_id):
    task = celery_app.AsyncResult(task_id)
    if task.state == "PENDING":
        return jsonify({"status": "Waiting in queue..."})
    elif task.state == "SUCCESS":
        return jsonify({"status": "Finished!", "result": task.result})
    else:
        return jsonify({"status": task.state})

if __name__ == "__main__":
    app.run(port=5000, debug=True)
```

#### How to test Flask:

1. **Terminal 1 (Worker):** `celery -A app.celery_app worker --loglevel=info`
2. **Terminal 2 (Flask):** `python app.py`
3. **Terminal 3 (Test):**
   ```bash
   curl -X POST http://127.0.0.1:5000/signup \
     -H "Content-Type: application/json" \
     -d '{"email": "alice@gmail.com"}'
   ```
   Copy the `task_id` from the output and check:
   ```bash
   curl http://127.0.0.1:5000/status/<TASK_ID>
   ```

### 2. Complete FastAPI Example

FastAPI is modern, fast, and uses Python type hints (`Pydantic`).

#### Directory Structure:

```text
fastapi_demo/
├── main.py
```

#### `main.py`:

```python
import time
from fastapi import FastAPI
from pydantic import BaseModel
from celery import Celery
from celery.result import AsyncResult

# 1. Initialize Celery
celery_app = Celery(
    "fastapi_worker",
    broker="redis://localhost:6379/0",
    backend="redis://localhost:6379/1"
)

# 2. Define background task
@celery_app.task
def generate_report(report_title: str):
    time.sleep(6)  # Simulate generating big PDF report
    return {"title": report_title, "download_url": f"https://cdn.site.com/{report_title}.pdf"}

# 3. Create FastAPI app
app = FastAPI(title="FastAPI + Celery Tutorial")

# Data schema for requests
class ReportRequest(BaseModel):
    title: str

# Route 1: Trigger task
@app.post("/reports/create", status_code=202)
def create_report(request: ReportRequest):
    # Offload to Celery
    task = generate_report.delay(request.title)
    return {
        "message": "Report generation started!",
        "task_id": task.id
    }

# Route 2: Check status
@app.get("/reports/status/{task_id}")
def get_report_status(task_id: str):
    task = AsyncResult(task_id, app=celery_app)
    return {
        "task_id": task_id,
        "is_ready": task.ready(),
        "status": task.state,
        "result": task.result if task.ready() else None
    }
```

#### How to test FastAPI:

1. **Terminal 1 (Worker):** `celery -A main.celery_app worker --loglevel=info`
2. **Terminal 2 (FastAPI):** `uvicorn main:app --port 8000 --reload`
3. **Open your browser at:** `http://localhost:8000/docs`
   - Use FastAPI's interactive Swagger interface to trigger `/reports/create`.
   - Take the returned `task_id` and test `/reports/status/{task_id}`!

### 3. Complete Django Example

Django uses a specialized decorator called `@shared_task` so you don't need to import the Celery `app` into every Django file.

#### 1. Add `celery.py` next to your `settings.py`:

```python
# myproject/myproject/celery.py
import os
from celery import Celery

# Tell Celery which settings file Django uses
os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'myproject.settings')

app = Celery('myproject')

# Read configuration from Django settings.py (keys starting with CELERY_)
app.config_from_object('django.conf:settings', namespace='CELERY')

# Automatically discover tasks in any installed Django app (tasks.py)
app.autodiscover_tasks()
```

#### 2. Configure `settings.py`:

```python
# myproject/myproject/settings.py
CELERY_BROKER_URL = 'redis://localhost:6379/0'
CELERY_RESULT_BACKEND = 'redis://localhost:6379/1'
CELERY_ACCEPT_CONTENT = ['json']
CELERY_TASK_SERIALIZER = 'json'
```

#### 3. Create `tasks.py` inside any Django app:

```python
# myproject/myapp/tasks.py
import time
from celery import shared_task

# Notice: @shared_task does not require importing 'app'!
@shared_task
def process_order(order_id):
    time.sleep(3)
    return f"Order #{order_id} has been processed!"
```

#### 4. Trigger inside any Django `views.py`:

```python
# myproject/myapp/views.py
from django.http import JsonResponse
from .tasks import process_order

def checkout_view(request):
    # Offload order processing to Celery worker
    task = process_order.delay(order_id=987)
    return JsonResponse({"status": "Order submitted", "task_id": task.id})
```

#### Run the Django Worker:

```bash
celery -A myproject worker --loglevel=info
```

---

## 8. Scaling Workers: From Local Machine to Real-World Production

What happens when your app grows from 10 tasks a day to 1,000,000 tasks an hour? You need more workers!

### The Kitchen Analogy

- One pizza chef can bake 1 pizza at a time.
- If 100 orders come in, pizzas take 3 hours to arrive.
- **Solution:** Bring 5 more chefs into the kitchen! All chefs pull order slips from the **same** order rack. Nobody bakes the same pizza twice.

In Celery, this is called the **Competing Consumers Pattern**:

```mermaid
flowchart TD
    Queue[("Broker Task Queue\n(Holds all tasks)")]

    subgraph WorkerFleet ["Fleet of Competing Workers"]
        W1["Worker 1 (Pulls Task #1)"]
        W2["Worker 2 (Pulls Task #2)"]
        W3["Worker 3 (Pulls Task #3)"]
        W4["Worker 4 (Pulls Task #4)"]
    end

    Queue -->|Pops task| W1
    Queue -->|Pops task| W2
    Queue -->|Pops task| W3
    Queue -->|Pops task| W4
```

Here is the step-by-step evolution of how scaling works from simple to production:

### Level 1: Scaling on a Single Machine (Concurrency)

When you start a worker, Celery spawns sub-processes managed by a master supervisor:

```text
               +-----------------------------+
               | Main Celery Supervisor Proc |
               +-----------------------------+
                /      |             |      \
               /       |             |       \
        +--------+ +--------+   +--------+ +--------+
        | Sub-1  | | Sub-2  |   | Sub-3  | | Sub-4  |
        +--------+ +--------+   +--------+ +--------+
```

You control the number of sub-processes with `--concurrency` (or `-c`):

```bash
# Run with 8 concurrent processes (can process 8 tasks at the same time)
celery -A tasks worker -c 8 --loglevel=info
```

#### Single-Machine Autoscaling:

Instead of a fixed number, Celery can automatically scale its sub-processes between a minimum and maximum based on workload:

```bash
# Keep 2 processes minimum, scale up to 10 if queue gets busy
celery -A tasks worker --autoscale=10,2 --loglevel=info
```

### Level 2: Multiple Worker Processes on the Same Machine

If you have a large server, you can launch distinct worker instances. Each instance must have a unique node name using `-n`:

```bash
# Terminal 1:
celery -A tasks worker -n worker_email@%h -Q emails --loglevel=info

# Terminal 2:
celery -A tasks worker -n worker_video@%h -Q heavy_video --loglevel=info
```

_(The `%h` gets replaced with your machine's hostname)._

### Level 3: Scaling with Docker Compose (Effortless Horizontal Scaling!)

When using Docker, you do not need to manage processes manually. You can scale your worker container with a single command!

In your `docker-compose.yml`:

```yaml
services:
  celery_worker:
    build: .
    command: celery -A tasks worker --loglevel=info
    depends_on:
      - redis
```

To run 5 worker containers simultaneously:

```bash
docker compose up --scale celery_worker=5
```

Docker will immediately boot up 5 identical worker containers! All 5 connect to the same Redis broker and pull tasks in parallel.

### Level 4: Real-World Production Management (Kubernetes & KEDA)

In modern cloud architectures (AWS, Google Cloud, Azure), workers run inside **Kubernetes (K8s)**.

```mermaid
flowchart LR
    Queue[("RabbitMQ / Redis\nQueue Length: 450 tasks")]
    KEDA["KEDA Autoscaler\nMonitors queue length"]
    Pods["Kubernetes Worker Pods\nScales from 1 to 20 pods!"]

    Queue -.->|Queue depth metric| KEDA
    KEDA -->|Tells K8s: 'Spin up more pods!'| Pods
    Pods -->|Process tasks| Queue
```

#### How Queue-Based Autoscaling Works (KEDA):

- **Normal traffic:** Queue has 0–5 tasks. K8s runs 1 worker pod (saving cloud bills).
- **Flash sale or traffic spike:** Queue jumps to 500 tasks.
- **KEDA (Kubernetes Event-driven Autoscaling):** Detects the queue length and automatically scales the number of worker pods up to 20.
- **Queue drains:** Once tasks hit 0, KEDA safely shrinks the worker count back down to 1.

### Managing Workers Remotely (Celery Control CLI)

Celery has built-in remote control commands to inspect and manage running workers in real-time from anywhere:

```bash
# 1. Check which workers are online and responding:
celery -A tasks status

# 2. See what tasks are currently running right now:
celery -A tasks inspect active

# 3. See how many tasks each worker has completed:
celery -A tasks inspect stats

# 4. Add 2 more subprocesses to a running worker without restarting it:
celery -A tasks control pool_grow 2

# 5. Shut down a worker gracefully after it finishes its current task:
celery -A tasks control shutdown
```

---

## 9. Production Best Practices & Monitoring

### Monitoring Tasks Visually with Flower

Instead of guessing what your workers are doing, you can run **Flower**, a live browser dashboard for Celery.

1. Install Flower:
   ```bash
   pip install flower
   ```
2. Start Flower:
   ```bash
   celery -A tasks flower --port=5555
   ```
3. Open `http://localhost:5555` in your browser.
   - View real-time graphs of completed and failed tasks.
   - Inspect task parameters, errors, and runtimes.
   - View worker CPU and memory usage.

### Production Golden Rules Checklist

1. **Keep Payloads Small:** Pass database IDs (e.g., `user_id=10`), never database model instances or open file objects.
2. **Always Set a Result Expiration (TTL):** Add `app.conf.result_expires = 3600` so Redis automatically discards old results after 1 hour.
3. **Turn Off Results for Fire-and-Forget:** If you don't need `result.get()`, add `@app.task(ignore_result=True)`.
4. **Always Plan for Failures:** Use `autoretry_for` with `retry_backoff=True` for any task communicating over a network.
5. **Tune Prefetch for Long Tasks:** If a task takes several minutes, set:
   ```python
   app.conf.worker_prefetch_multiplier = 1
   app.conf.task_acks_late = True
   ```
   This ensures workers only pull one task at a time, and if a worker server crashes, the task is safely returned to the queue!
