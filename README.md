# Blade

Blade is an experimental AI agent built by ItzRustam to learn and experiment with **agentic AI, tool calling, and LLM-based task orchestration**.

Instead of only generating text, Blade can decide when a tool is needed, execute that tool, process the result, and continue reasoning until the user's request is completed.

## Features

* LLM-powered agent
* Tool calling and tool selection
* Custom ReAct-style agent loop
* Web search
* File creation and reading
* File searching
* Python code execution
* Multi-step tool execution
* Conversation history during a session
* Configurable maximum tool usage
* Designed to minimize unnecessary tool calls

## Available Tools

Blade currently has tools for:

* `web_search` — search the web
* `create_file` — create files
* `read_file` — read files
* `find_file` — find files
* `run_python_code` — execute Python code
* `get_text_length` — calculate text length

More tools can be added as the project evolves.

## How It Works

Blade uses an LLM to determine whether a tool is required for the user's request.

```text
User
  │
  ▼
Blade
  │
  ▼
LLM
  │
  ├── No tool needed ──► Final response
  │
  └── Tool needed
          │
          ▼
      Tool execution
          │
          ▼
      Tool result
          │
          ▼
         LLM
          │
          ▼
      Final response
```

The agent does not blindly call every available tool. It is instructed to select the appropriate tool and use the minimum number of calls necessary to complete the task.

## Example

For a request such as:

```text
Search for rslearn-ML and rsroute from ItzRustam GitHub
```

Blade can:

1. Determine that web search is required.
2. Select the `web_search` tool.
3. Execute the search.
4. Process the returned information.
5. Perform another search if additional information is actually needed.
6. Return the final answer.

Another example:

```text
Find NVIDIA GPUs that support CUDA and save the information to cuda_gpu.txt
```

Blade can combine web search and file creation to complete the task.

## Tech Stack

Blade is built primarily with the LangChain ecosystem.

* **Python**
* **LangChain**
* **LangChain Core**
* **LangChain Google GenAI**
* **DDGS** — web search
* **python-dotenv** — environment configuration
* **Rich** — terminal output

Main packages:

```text
langchain
langchain-core
langchain-google-genai
ddgs
python-dotenv
rich
```

## Installation

Clone the repository and install the dependencies:

```bash
git clone https://www.github.com/ItzRustam/Blade
cd Blade

pip install -r requirements.txt
```

Using a virtual environment is recommended:

```bash
python -m venv .venv
source .venv/bin/activate

pip install -r requirements.txt
```

## Configuration

Create a `.env` file in the project root.

```env
MODEL=your-model-name
GOOGLE_API_KEY=your-google-api-key
MAX_TOOL_USE=10 # Increase it if you are doing advance Tasks
USER_NAME="your_name"
```

`MODEL` specifies the model Blade should use, while `MAX_TOOL_USE` limits how many tool calls the agent can make during a request.

## Usage

Start Blade with:

```bash
python main.py
```

Then enter your requests in the terminal.

Example:

```text
You: Search for rslearn-ML on GitHub
```

To stop Blade:

```text
You: exit
```

## Project Structure

```text
Blade/
├── blade/
│   ├── tools/
│   ├── agent.py
│   └── prompts.py
│
├── main.py
├── requirements.txt
├── .env
└── README.md
```

The project structure may change as Blade develops.

## NOTE
Blade works will be saved into his own Workspace named `agent_workspace` to prevent harming system files.

## Why I Built Blade

Blade is primarily a **learning project**.

The goal is to understand how agentic systems work internally instead of relying entirely on high-level agent frameworks.

The project explores concepts such as:

* Tool calling
* Tool selection
* ReAct-style loops
* Agent memory
* Multi-step execution
* Tool-result handling
* Agent stopping conditions
* Reducing unnecessary tool calls
* LLM-driven task orchestration

## Project Status

Blade is an experimental project and is actively being developed.

The architecture and available tools may change as I experiment with different approaches to building AI agents.

---

**Built by ItzRustam while learning Agentic AI.**
