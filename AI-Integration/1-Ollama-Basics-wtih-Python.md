# Ollama Complete Tutorial Notes & In-Depth Reference Guide

> **Source Video:** [Learn Ollama in 15 Minutes - Run LLM Models Locally for FREE](https://www.youtube.com/watch?v=UtSSMs6ObqY&t=624s)  
> **Creator:** Tech With Tim  
> **Companion Repository:** [`techwithtim/OllamaTutorial`](https://github.com/techwithtim/OllamaTutorial)  
> **Bookmarked Section:** `10:24` (`t=624s`) — _Ollama Python Package_

---

## Table of Contents

1. [Overview & Core Architecture](#1-overview--core-architecture)
   - [What is Ollama?](#what-is-ollama)
   - [How It Works Under the Hood (`llama.cpp` & GGUF)](#how-it-works-under-the-hood-llamacpp--gguf)
   - [Cloud APIs vs. Local Ollama: Architectural Trade-Offs](#cloud-apis-vs-local-ollama-architectural-trade-offs)
   - [VRAM & Hardware Sizing Math](#vram--hardware-sizing-math)
2. [Installation & Daemon Architecture](#2-installation--daemon-architecture)
   - [Installing Across Platforms](#installing-across-platforms)
   - [The Ollama Background Service](#the-ollama-background-service)
   - [Critical Environment Variables](#critical-environment-variables)
3. [Running & Managing Models Locally (CLI)](#3-running--managing-models-locally-cli)
   - [Interactive REPL with `ollama run`](#interactive-repl-with-ollama-run)
   - [Pre-downloading with `ollama pull`](#pre-downloading-with-ollama-pull)
   - [Model Tags, Quantization, and Instruct Variants](#model-tags-quantization-and-instruct-variants)
4. [Managing Multiple Models & Memory Lifecycle](#4-managing-multiple-models--memory-lifecycle)
   - [Inspecting Models (`ollama list` and `ollama show`)](#inspecting-models-ollama-list-and-ollama-show)
   - [Active Memory Management (`ollama ps` & VRAM Offloading)](#active-memory-management-ollama-ps--vram-offloading)
   - [Removing Models (`ollama rm`)](#removing-models-ollama-rm)
5. [Ollama HTTP REST API Deep-Dive](#5-ollama-http-rest-api-deep-dive)
   - [Why an HTTP Server Layer?](#why-an-http-server-layer)
   - [Endpoints: `/api/generate` vs. `/api/chat`](#endpoints-apigenerate-vs-apichat)
   - [Understanding NDJSON Streaming](#understanding-ndjson-streaming)
6. [Calling the HTTP API in Python (`requests`)](#6-calling-the-http-api-in-python-requests)
   - [Step-by-Step Code Walkthrough (`sample_request.py`)](#step-by-step-code-walkthrough-sample_requestpy)
   - [Why `iter_lines()` and `flush=True` Matter](#why-iter_lines-and-flushtrue-matter)
   - [Non-Streaming Implementation](#non-streaming-implementation)
7. [Official Ollama Python Library (`ollama-python`)](#7-official-ollama-python-library-ollama-python)
   - [Why Use the SDK over Raw HTTP?](#why-use-the-sdk-over-raw-http)
   - [Basic Generation (`package.py`)](#basic-generation-packagepy)
   - [Structured Multi-Turn Chat](#structured-multi-turn-chat)
   - [Streaming via SDK](#streaming-via-sdk)
   - [Asynchronous Client (`AsyncClient`)](#asynchronous-client-asyncclient)
8. [Customizing Models with `Modelfile`](#8-customizing-models-with-modelfile)
   - [The "Docker for LLMs" Concept](#the-docker-for-llms-concept)
   - [Modelfile Directives & Hyperparameters Explained](#modelfile-directives--hyperparameters-explained)
   - [Building, Tagging, and Running Custom Models](#building-tagging-and-running-custom-models)
9. [Architecture Guide: Wrapping Ollama in Production APIs](#9-architecture-guide-wrapping-ollama-in-production-apis)
   - [Example: Fast, Authenticated API with FastAPI](#example-fast-authenticated-api-with-fastapi)
10. [Quick CLI & API Cheat Sheet](#10-quick-cli--api-cheat-sheet)

---

## 1. Overview & Core Architecture

### What is Ollama?

**Ollama** is an open-source model execution runtime, distribution tool, and package manager tailored specifically for open-weight Large Language Models (LLMs). Rather than requiring developers to manually manage weight files, Python virtual environments, PyTorch/CUDA driver bindings, and quantization libraries, Ollama packages the complete stack into a single unified binary and background daemon.

### How It Works Under the Hood (`llama.cpp` & GGUF)

To understand why Ollama is fast and lightweight, it helps to understand its underlying architecture:

```
+----------------------------------------------------------------+
|                         Your Application                       |
|           (Terminal CLI / Python SDK / Web App / REST API)     |
+----------------------------------------------------------------+
                               |
                               v (HTTP / REST on :11434)
+----------------------------------------------------------------+
|                        Ollama Daemon                           |
|   - Model Registry & Layer Management                          |
|   - Request Queuing & Scheduling                               |
|   - Memory / Keep-Alive Lifecycle                              |
+----------------------------------------------------------------+
                               |
                               v
+----------------------------------------------------------------+
|                    Inference Engine (llama.cpp)                |
|   - Executes GGUF Quantized Models                             |
|   - Hardware Acceleration: Apple Metal / NVIDIA CUDA / CPU     |
+----------------------------------------------------------------+
```

1. **Inference Core (`llama.cpp`):**
   Ollama is powered by `llama.cpp`, a highly optimized C/C++ inference engine developed by Georgi Gerganov. Unlike Python-based inference engines that carry interpreter overhead and massive CUDA dependencies, `llama.cpp` runs directly on bare-metal hardware.
2. **The GGUF Format:**
   Ollama models are stored and served as **GGUF** (GPT-Generated Unified Format) binary files. GGUF stores both model metadata (vocabulary, tokenizer configs, context limits) and tensor weights in one contiguous, memory-mappable file.
3. **Hardware Acceleration Out-of-the-Box:**
   - **Apple Silicon (M1/M2/M3/M4):** Uses Apple's unified memory architecture via **Metal**, allowing the GPU and Neural Engine to read weights directly from system RAM without PCIe data bus copy penalties.
   - **NVIDIA GPUs:** Automatically compiles and loads CUDA kernels to offload tensor math to Tensor Cores.
   - **x86 / ARM CPUs:** Utilizes AVX, AVX2, and AVX-512 vector instructions for machines without dedicated graphics cards.

### Cloud APIs vs. Local Ollama: Architectural Trade-Offs

| Dimension                     | Cloud LLM APIs (OpenAI, Anthropic, Gemini)                                   | Local Ollama Runtime                                                                                          |
| :---------------------------- | :--------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------ |
| **Data Privacy & Compliance** | Prompts and responses leave perimeter; subject to vendor retention policies. | **100% On-Premise.** Zero data leaves the local machine or internal subnet (HIPAA/GDPR compliant by default). |
| **Cost Model**                | Pay per 1K/1M tokens consumed; can spike unexpectedly with traffic.          | **Fixed Infrastructure Cost.** Zero per-token charges, completely free after hardware acquisition.            |
| **Network Dependency**        | Dependent on active internet connection and vendor uptime.                   | **Fully Offline.** Runs without internet; immune to cloud outages.                                            |
| **Latency & Throughput**      | Network round-trip latency + queue wait times.                               | **Zero Network Overhead.** First-token latency bounded only by local compute power.                           |
| **Model Customization**       | Restricted to vendor fine-tuning endpoints and system prompts.               | **Total Control.** Modify parameters, system personas, context windows, and run raw open weights.             |

### VRAM & Hardware Sizing Math

The parameter count and quantization level directly dictate how much RAM or VRAM is required to load and run a model comfortably:

$$\text{Estimated VRAM (GB)} \approx \frac{\text{Parameter Count (Billions)} \times \text{Bits per Weight}}{8} \times 1.25$$

_(The 1.25 multiplier accounts for the KV-cache and context memory overhead)._

- **1B – 3B Models** (`llama3.2:1b`, `llama3.2:3b`, `phi3:mini`):
  - Requires **2 GB to 4 GB** VRAM/RAM.
  - Runs smoothly on low-power laptops, Raspberry Pi 5, or older workstations.
- **7B – 8B Models** (`llama3.1:8b`, `mistral:7b`, `gemma2:9b`):
  - Requires **6 GB to 8 GB** VRAM/RAM (at 4-bit quantization).
  - Ideal sweet spot for standard developer laptops (e.g., 16 GB Apple Silicon Mac or 8 GB NVIDIA RTX GPU).
- **14B – 32B Models** (`qwen2.5-coder:14b`, `qwen2.5:32b`):
  - Requires **12 GB to 24 GB** VRAM/RAM.
  - High-accuracy reasoning and coding; requires higher-end GPUs (RTX 3090/4090) or 24 GB–36 GB unified memory Macs.
- **70B Models** (`llama3.1:70b`):
  - Requires **40 GB to 48 GB+** VRAM/RAM.
  - High-performance enterprise grade; requires multi-GPU or 64 GB–128 GB Mac Studio.

---

## 2. Installation & Daemon Architecture

### Installing Across Platforms

Download installer packages from [ollama.com/download](https://ollama.com/download):

- **macOS:** Installs `/Applications/Ollama.app` and links the CLI binary to `/usr/local/bin/ollama`.
- **Linux:** One-line shell installer (`curl -fsSL https://ollama.com/install.sh | sh`) that configures a `systemd` unit.
- **Windows:** Installs a Windows background tray utility and configures system environment paths.

### The Ollama Background Service

When installed, Ollama does not just provide a CLI tool—it spawns a persistent daemon process.
Verify that the daemon is listening:

```bash
ollama --version
```

To check if the underlying HTTP server is accepting connections:

```bash
curl http://localhost:11434
# Returns: Ollama is running
```

### Critical Environment Variables

You can configure the daemon behavior using environment variables:

| Environment Variable       | Default Value      | Description                                                                                        |
| :------------------------- | :----------------- | :------------------------------------------------------------------------------------------------- |
| `OLLAMA_HOST`              | `127.0.0.1:11434`  | Change to `0.0.0.0:11434` to expose Ollama to local network/Docker containers.                     |
| `OLLAMA_MODELS`            | `~/.ollama/models` | Custom storage location for downloaded model weights (useful if OS drive is small).                |
| `OLLAMA_KEEP_ALIVE`        | `5m`               | Duration a model stays resident in VRAM before auto-unloading (`-1` keeps it loaded indefinitely). |
| `OLLAMA_NUM_PARALLEL`      | `1`                | Number of simultaneous user requests a single model can process concurrently.                      |
| `OLLAMA_MAX_LOADED_MODELS` | `1`                | Maximum number of distinct models loaded simultaneously in memory.                                 |

> **Tip for macOS users:** Environment variables for the GUI app can be set via `launchctl setenv OLLAMA_HOST "0.0.0.0:11434"`.

---

## 3. Running & Managing Models Locally (CLI)

### Interactive REPL with `ollama run`

The primary command to start chatting with a model is:

```bash
ollama run mistral
```

```bash
ollama run llama3.2
```

#### What happens behind the scenes?

1. **Cache Inspection:** Ollama checks `~/.ollama/models/manifests` to see if the requested tag exists locally.
2. **Automatic Pull:** If absent, it queries the Ollama registry (`registry.ollama.ai`), downloads the layer manifests, and streams the GGUF blobs with a terminal progress bar.
3. **VRAM Layer Offloading:** It analyzes your hardware (available GPU memory vs. system RAM) and allocates as many transformer layers as possible directly into VRAM.
4. **REPL Session:** It opens a terminal Read-Eval-Print Loop where you can converse directly with the LLM.

#### In-Session REPL Controls:

- `/bye` or `Ctrl + D`: Gracefully exits the session and initiates the keep-alive countdown.
- `/?`: Displays interactive commands.
- `/? shortcuts`: Lists hotkeys.
- `"""`: Multi-line prompt mode (press Enter inside triple quotes without submitting).

### Pre-downloading with `ollama pull`

To download weights in advance (e.g., in automated setup scripts or CI/CD) without opening a prompt:

```bash
ollama pull llama3.2
ollama pull mistral
```

### Model Tags, Quantization, and Instruct Variants

Model names in Ollama follow a container-like registry naming convention: `name:tag`.

```
model-name : parameter-size - type - quantization
llama3.1   :     8b       - instruct - q4_0
```

- **Tag Defaults:** Running `ollama run llama3` defaults to `llama3:latest` (usually the 4-bit quantized instruct version).
- **Instruct vs. Base:**
  - _Base Models_ (`model:text`): Raw text continuations; not trained for dialogue.
  - _Instruct/Chat Models_ (default): Supervised Fine-Tuned (SFT) and aligned via RLHF/DPO to follow conversational commands.
- **Quantization Types:**
  - `q4_0` / `q4_K_M` (4-bit): ~75% reduction in size compared to 16-bit float, with negligible degradation in reasoning.
  - `q8_0` (8-bit): Higher fidelity, closer to native FP16; requires ~2x VRAM compared to 4-bit.
  - `fp16` (16-bit): Full precision; requires substantial VRAM.

---

## 4. Managing Multiple Models & Memory Lifecycle

### Inspecting Models (`ollama list` and `ollama show`)

List all models currently saved to the local disk:

```bash
ollama list
```

_Output columns include: `NAME`, `ID`, `SIZE`, and `MODIFIED`._

Inspect the internal architecture, tokenizer, parameters, and system prompt of a model:

```bash
ollama show mistral
ollama show --modelfile llama3.2
ollama show --parameters llama3.2
```

### Active Memory Management (`ollama ps` & VRAM Offloading)

One of Ollama's most critical features is how it balances GPU and CPU memory:

```bash
ollama ps
```

Example output:

```
NAME            ID              SIZE      PROCESSOR    UNTIL
llama3.2:latest a849d4f0d610    2.0 GB    100% GPU     4 minutes from now
```

#### Understanding the `PROCESSOR` column:

- **`100% GPU`:** The entire neural network fits into graphics VRAM. Token generation will be at maximum possible speed (e.g., 50–120 tokens/sec on Apple Silicon or modern RTX).
- **`Partial GPU / CPU (e.g. 60% / 40%)`:** The model is too large for your VRAM. Ollama splits the layers, calculating some on GPU and some on CPU. This avoids out-of-memory crashes, but speeds will be bottlenecked by PCIe bus transfer bandwidth.
- **`100% CPU`:** No GPU acceleration detected or memory exhausted; computed purely via CPU AVX instructions.

#### The Keep-Alive Timer:

Once an inference call completes, the model remains loaded in memory for **5 minutes** by default (`UNTIL` column). If another prompt arrives within 5 minutes, response generation begins immediately without reload latency. After 5 minutes of idle time, Ollama purges the weights from VRAM to make room for other applications.

### Removing Models (`ollama rm`)

To reclaim storage space:

```bash
ollama rm mistral
```

---

## 5. Ollama HTTP REST API Deep-Dive

### Why an HTTP Server Layer?

Ollama runs an internal HTTP web server listening on port `11434`. This architecture enables complete language and process decoupling:

- Your application does not need to link against C++ binaries or run inside a specific Python environment.
- Any tool capable of making an HTTP POST request (cURL, Python `requests`, Node.js `fetch`, Go, Rust, mobile apps) can leverage local LLMs.

```
+-------------------+           HTTP POST /api/chat           +-------------------+
|  Python Backend   | --------------------------------------> |   Ollama Daemon   |
| (FastAPI / Flask) | <-------------------------------------- | (localhost:11434) |
+-------------------+           NDJSON Streaming Chunks       +-------------------+
```

### Endpoints: `/api/generate` vs. `/api/chat`

#### 1. `/api/generate` (Raw Completion)

Used when you want raw continuation of a single prompt string without conversational context:

- **Endpoint:** `POST http://localhost:11434/api/generate`
- **Payload:**
  ```json
  {
    "model": "mistral",
    "prompt": "Write a haiku about servers.",
    "stream": false
  }
  ```

#### 2. `/api/chat` (Structured Multi-Turn Dialogue)

Used for structured conversations with role-based histories (`system`, `user`, `assistant`). Ollama automatically formats these messages with the model's native chat template (applying appropriate delimiters like `<|im_start|>` or `[INST]`):

- **Endpoint:** `POST http://localhost:11434/api/chat`
- **Payload:**
  ```json
  {
    "model": "mistral",
    "messages": [
      { "role": "system", "content": "You are a senior database architect." },
      { "role": "user", "content": "Explain index fragmentation." }
    ],
    "stream": true
  }
  ```

### Understanding NDJSON Streaming

Large Language Models generate text sequentially, token-by-token. Generating a 400-word response can take 2 to 8 seconds depending on hardware.

Rather than making the client wait in silence until the full text is generated, Ollama uses **Newline-Delimited JSON (NDJSON)**:

- Each HTTP chunk sent over the TCP connection is a self-contained, valid JSON object ending with a newline character (`\n`).
- The client reads and parses each line as it arrives, rendering tokens to the user in real time.

#### Anatomy of a Stream Chunk:

```json
{
  "model": "mistral",
  "created_at": "2026-09-13T06:30:00Z",
  "message": { "role": "assistant", "content": "Database" },
  "done": false
}
```

When finished, the final chunk sets `"done": true` and attaches performance statistics:

```json
{
  "model": "mistral",
  "done": true,
  "total_duration": 1823450200,
  "load_duration": 451200,
  "prompt_eval_count": 24,
  "prompt_eval_duration": 112300000,
  "eval_count": 185,
  "eval_duration": 1710699000
}
```

_Notice: $\text{Tokens per second} = \frac{\text{eval\_count}}{\text{eval\_duration (in seconds)}} = \frac{185}{1.71} \approx 108.18\text{ tokens/sec}$._

---

## 6. Calling the HTTP API in Python (`requests`)

Direct HTTP requests using Python's standard `requests` library allow you to integrate Ollama without installing extra SDK dependencies.

### Step-by-Step Code Walkthrough (`sample_request.py`)

Below is the exact script demonstrated in the tutorial, annotated with explanations:

```python
import requests
import json

# 1. Base URL for local Ollama API
url = "http://localhost:11434/api/chat"

# 2. Define the conversation payload
payload = {
    "model": "mistral",  # Target model tag
    "messages": [
        {"role": "user", "content": "What is Python?"}
    ]
    # "stream": True is implicit by default in Ollama
}

# 3. Send HTTP POST request with streaming enabled
# CRITICAL: stream=True tells urllib3 not to buffer the full response body in memory
response = requests.post(url, json=payload, stream=True)

# 4. Handle response
if response.status_code == 200:
    print("Streaming response from Ollama:")

    # iter_lines() iterates over response lines as they arrive over the socket
    for line in response.iter_lines(decode_unicode=True):
        if line:  # Filter out keep-alive heartbeat newlines
            try:
                # Parse each individual line as its own JSON object
                json_data = json.loads(line)

                # Extract the partial token chunk from the assistant's message
                if "message" in json_data and "content" in json_data["message"]:
                    # end="" prevents printing a newline after every word
                    # flush=True forces the terminal stdout buffer to flush immediately
                    print(json_data["message"]["content"], end="", flush=True)
            except json.JSONDecodeError:
                print(f"\nFailed to parse line: {line}")
    print()  # Add final newline once generation completes
else:
    print(f"Error {response.status_code}: {response.text}")
```

### Why `iter_lines()` and `flush=True` Matter

1. **`response.iter_lines(decode_unicode=True)`:**
   Without `iter_lines()`, reading `response.text` forces Python to wait until the entire response stream closes before returning anything. `iter_lines()` yields chunks line-by-line as they travel down the socket.
2. **`flush=True`:**
   By default, Python buffers console output and only prints when a newline (`\n`) is encountered. Because partial tokens do not contain newlines, setting `flush=True` guarantees that words appear on the screen the millisecond they are generated.

### Non-Streaming Implementation

If your use case does not need real-time streaming (such as an automated data extraction pipeline or background batch job), pass `"stream": false`:

```python
import requests

response = requests.post(
    "http://localhost:11434/api/chat",
    json={
        "model": "mistral",
        "messages": [{"role": "user", "content": "Give me 3 bullet points on Git."}],
        "stream": False  # Disable streaming
    }
)

if response.status_code == 200:
    data = response.json()
    # Entire reply is already collected in the content field
    print(data["message"]["content"])
```

---

## 7. Official Ollama Python Library (`ollama-python`)

_(Video Timestamp: `10:24` / `t=624s`)_

While raw HTTP works, the official Python library (`ollama`) provides a cleaner, type-safe, and more maintainable interface.

### Why Use the SDK over Raw HTTP?

- **Automatic Session & Connection Pooling:** Reuses persistent HTTP keep-alive connections.
- **Strong Typing & Auto-completion:** Returns structured dictionaries/objects with IDE autocomplete.
- **Built-in Stream Handling:** Returns native Python generators instead of requiring manual line-by-line JSON parsing.
- **Built-in Client Lifecycle:** Simplifies model pulling, deletion, and parameter injection.

### Installation

```bash
pip install ollama
```

### Basic Generation (`package.py`)

```python
import ollama

# Initialize the client (connects to http://localhost:11434 by default)
client = ollama.Client()

model = "llama2"  # or llama3.2, mistral, etc.
prompt = "What is Python?"

# Send synchronous generation request
response = client.generate(model=model, prompt=prompt)

# Clean, structured access to generated response
print("Response from Ollama:")
print(response.response)
```

### Structured Multi-Turn Chat

```python
import ollama

# Multi-turn conversation maintaining role history
messages = [
    {"role": "system", "content": "You are an expert Python tutor."},
    {"role": "user", "content": "What is a decorator in Python?"}
]

response = ollama.chat(model="llama3.2", messages=messages)

# Append assistant response to keep conversation history alive
reply = response["message"]["content"]
print("Assistant:", reply)

messages.append({"role": "assistant", "content": reply})
messages.append({"role": "user", "content": "Can you give me a simple code example of that?"})

follow_up = ollama.chat(model="llama3.2", messages=messages)
print("Follow-up:", follow_up["message"]["content"])
```

### Streaming via SDK

With the SDK, streaming requires no manual JSON parsing. Setting `stream=True` returns an iterator yielding chunk objects:

```python
import ollama

stream = ollama.chat(
    model="llama3.2",
    messages=[{"role": "user", "content": "Write a short poem about coding."}],
    stream=True
)

for chunk in stream:
    # Directly read the incremental token
    print(chunk["message"]["content"], end="", flush=True)
print()
```

### Asynchronous Client (`AsyncClient`)

When integrating with asynchronous frameworks like **FastAPI** or **Tornado**, blocking synchronous calls can freeze the entire web server event loop. Use `ollama.AsyncClient`:

```python
import asyncio
import ollama

async def main():
    client = ollama.AsyncClient()
    response = await client.chat(
        model="llama3.2",
        messages=[{"role": "user", "content": "Hello Async!"}]
    )
    print(response["message"]["content"])

asyncio.run(main())
```

---

## 8. Customizing Models with `Modelfile`

### The "Docker for LLMs" Concept

A `Modelfile` is the blueprint used to build custom local LLM variants. Just as a `Dockerfile` defines base OS images, environment variables, and entry points, a `Modelfile` specifies:

1. Which foundational weights to inherit from (`FROM`).
2. What persona and behavior rules to enforce (`SYSTEM`).
3. What mathematical constraints to place on sampling (`PARAMETER`).

```
+-------------------------------------------------------------+
|                          Modelfile                          |
|                                                             |
|  FROM llama3.2                                              |
|  PARAMETER temperature 1                                    |
|  SYSTEM "You are Mario from Super Mario Bros..."            |
+-------------------------------------------------------------+
                               |
                               v (ollama create mario -f ./Modelfile)
+-------------------------------------------------------------+
|                     Custom Model: 'mario'                   |
|  - Shares underlying llama3.2 weights (zero disk duplicate) |
|  - Encapsulates Mario persona and temperature parameters    |
+-------------------------------------------------------------+
```

### Modelfile Directives & Hyperparameters Explained

```dockerfile
# 1. Base model to inherit weights and architecture from
FROM llama3.2

# 2. Model parameters (sampling hyperparameters)
PARAMETER temperature 1
PARAMETER top_p 0.9
PARAMETER num_ctx 4096

# 3. System prompt to define persona, rules, and guardrails
SYSTEM """
You are Mario from Super Mario Bros. Answer as Mario, the assistant, only.
"""
```

#### Detailed Breakdown of Hyperparameters:

- **`PARAMETER temperature <float>` (Default: `0.8`, Range: `0.0` - `2.0`):**
  - Controls the randomness of the model's token selection.
  - **Low (0.1 – 0.3):** Highly deterministic, logical, and repetitive. Best for mathematical calculation, coding, JSON generation, and factual classification.
  - **Medium (0.7 – 0.8):** Balanced fluency and natural tone; ideal for conversational chatbots.
  - **High (1.0 – 1.5):** Creative, erratic, and varied. Great for creative writing, brainstorming, and roleplay (e.g., the Mario persona).
- **`PARAMETER top_p <float>` (Default: `0.9`):**
  - Nucleus sampling: The model only selects tokens from the top $P$ percentage of probability distribution. A lower `top_p` (e.g., `0.5`) filters out obscure and strange words.
- **`PARAMETER top_k <int>` (Default: `40`):**
  - Reduces the probability of generating nonsensical tokens by restricting choices to the top $K$ most likely candidates.
- **`PARAMETER num_ctx <int>` (Default: `2048`):**
  - Sets the size of the context window (how many tokens of conversation history and prompt the model can remember at once).
  - _Note:_ Raising `num_ctx` to `8192` or `32768` allows large document ingestion, but increases memory (RAM/VRAM) allocation for the KV-cache.
- **`PARAMETER stop "<string>"`:**
  - Defines explicit stop sequences that immediately halt token generation (useful for preventing agent loop runaway).

### Building, Tagging, and Running Custom Models

1. **Create the file:** Save the code above as `Modelfile` in your directory.
2. **Build the custom model:**
   ```bash
   ollama create mario -f ./Modelfile
   ```
   _Note: Ollama does not duplicate the gigabytes of base model weights on your hard drive; it creates a lightweight pointer manifest with your custom prompt and parameter overlay._
3. **Run and test the custom persona:**
   ```bash
   ollama run mario
   ```
   _Prompt:_ "What should I do if Bowser kidnaps the Princess?"  
   _Response:_ "Mamma Mia! Don't you worry! Put on your overalls, grab a Super Mushroom, and let's-a go rescue Princess Peach!"
4. **Use in Python code:**

   ```python
   import ollama

   response = ollama.chat(
       model="mario",
       messages=[{"role": "user", "content": "Who is Luigi?"}]
   )
   print(response["message"]["content"])
   ```

---

## 9. Architecture Guide: Wrapping Ollama in Production APIs

One of the most practical applications of Ollama is wrapping your local models in a custom REST or GraphQL API (using frameworks like **FastAPI**). This enables you to:

- Enforce API key authentication and usage quotas.
- Add metering or rate limits.
- Sanitize and validate inputs with Pydantic schemas.
- Expose local AI models to web frontends or internal microservices.

### Example: Fast, Authenticated API with FastAPI

Here is an architectural pattern showing how Ollama connects into a secure web service:

```python
from fastapi import FastAPI, Header, Depends, HTTPException
from pydantic import BaseModel
import ollama
import os

app = FastAPI(title="Local LLM Gateway API")

# Mock database of API keys with available usage credits
API_KEY_CREDITS = {
    "secret-user-key-123": 10,
    "admin-key-456": 100
}

# Request body schema
class PromptRequest(BaseModel):
    prompt: str
    model: str = "llama3.2"  # or custom model like "mario"

# Dependency to authenticate and check credit balance
def verify_api_key_and_credits(x_api_key: str = Header(None)):
    if not x_api_key or x_api_key not in API_KEY_CREDITS:
        raise HTTPException(status_code=401, detail="Invalid or missing API key.")

    credits_left = API_KEY_CREDITS[x_api_key]
    if credits_left <= 0:
        raise HTTPException(status_code=403, detail="Credit balance exhausted.")

    return x_api_key

@app.post("/v1/chat")
def chat_completion(
    request: PromptRequest,
    api_key: str = Depends(verify_api_key_and_credits)
):
    # Deduct 1 credit per generation
    API_KEY_CREDITS[api_key] -= 1

    # Forward query to local Ollama daemon
    try:
        response = ollama.chat(
            model=request.model,
            messages=[{"role": "user", "content": request.prompt}]
        )
        return {
            "model": request.model,
            "response": response["message"]["content"],
            "credits_remaining": API_KEY_CREDITS[api_key]
        }
    except Exception as e:
        # Refund credit if local inference fails
        API_KEY_CREDITS[api_key] += 1
        raise HTTPException(status_code=500, detail=f"Ollama inference error: {str(e)}")
```

---

## 10. Quick CLI & API Cheat Sheet

### Terminal CLI Commands

| Task              | Command                          | Description                                       |
| :---------------- | :------------------------------- | :------------------------------------------------ |
| **Run / Chat**    | `ollama run <model>`             | Pulls (if missing) and launches interactive REPL. |
| **Pre-download**  | `ollama pull <model>`            | Downloads weights without opening REPL.           |
| **List Models**   | `ollama list`                    | Shows all downloaded local models and sizes.      |
| **Active Models** | `ollama ps`                      | Shows models currently loaded in RAM/VRAM.        |
| **Inspect Model** | `ollama show <model>`            | Shows architecture, context size, and template.   |
| **Delete Model**  | `ollama rm <model>`              | Deletes model from disk to reclaim storage.       |
| **Build Model**   | `ollama create <name> -f <file>` | Compiles a custom model from a `Modelfile`.       |
| **Copy Tag**      | `ollama cp <src> <dest>`         | Duplicates/renames a model tag.                   |

### REST API Endpoints Reference (`http://localhost:11434`)

| Method   | Endpoint        | Purpose         | Key Payload Fields                               |
| :------- | :-------------- | :-------------- | :----------------------------------------------- |
| `POST`   | `/api/generate` | Raw completion  | `model`, `prompt`, `stream`, `options`           |
| `POST`   | `/api/chat`     | Structured chat | `model`, `messages: [{role, content}]`, `stream` |
| `GET`    | `/api/tags`     | List models     | None                                             |
| `POST`   | `/api/show`     | Inspect model   | `name`                                           |
| `DELETE` | `/api/delete`   | Delete model    | `name`                                           |
