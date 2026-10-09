# 🔎 AI Research Assistant

An agentic AI research assistant built with **Python, LangChain, Google Gemini, and Streamlit**.

The assistant can decide when to use web search, webpage fetching, or mathematical calculations, then synthesize the collected information into a final answer with a curated list of relevant sources.

## Features

* 🤖 Agentic tool selection using Google Gemini
* 🔎 Web search for current and externally verifiable information
* 🌐 Webpage fetching when deeper page analysis is required
* 🧮 Calculator tool for mathematical questions
* 📚 Automatic source collection
* 🎯 AI-powered source selection
* 🔗 Clickable sources in the Streamlit interface
* ⏳ Real-time research progress
* 🛑 Maximum tool-call limit for controlled execution
* 💻 Streamlit web interface
* 🖥️ CLI interface
* 🔐 Environment-variable based API configuration

## Architecture

```text
                         ┌─────────────────────┐
                         │       User          │
                         └──────────┬──────────┘
                                    │
                                    ▼
                         ┌─────────────────────┐
                         │   Research Agent   │
                         │     Gemini LLM      │
                         └──────────┬──────────┘
                                    │
                 ┌──────────────────┼──────────────────┐
                 │                  │                  │
                 ▼                  ▼                  ▼
          ┌─────────────┐    ┌─────────────┐    ┌─────────────┐
          │ web_search  │    │  web_fetch  │    │ calculator  │
          └──────┬──────┘    └──────┬──────┘    └─────────────┘
                 │                  │
                 └──────────┬───────┘
                            ▼
                    ┌───────────────┐
                    │ Source        │
                    │ Collection    │
                    └───────┬───────┘
                            ▼
                    ┌───────────────┐
                    │ Source        │
                    │ Selection     │
                    └───────┬───────┘
                            ▼
                    ┌───────────────┐
                    │ Final Answer  │
                    │ + Sources     │
                    └───────────────┘
```

## Project Structure

```text
ai-research-agent/
│
├── app.py
├── main.py
├── agent.py
├── requirements.txt
├── .env.example
├── .gitignore
├── README.md
│
└── tools/
    ├── __init__.py
    ├── calculator.py
    ├── web_search.py
    └── web_fetch.py
```

## How It Works

### 1. User Query

The user submits a research question through either the Streamlit interface or the command-line interface.

### 2. Tool Selection

Gemini determines whether external tools are required.

The available tools are:

* `web_search`
* `web_fetch`
* `calculator`

The agent is instructed not to use tools unnecessarily.

### 3. Web Research

For current or externally verifiable information, the agent can use `web_search`.

`web_fetch` is only used when the actual contents of a webpage are required.

### 4. Source Collection

Search results are parsed and unique URLs are collected during the research process.

### 5. Source Selection

After the research is complete, Gemini evaluates the collected sources and selects the sources most relevant to the final answer.

The selection prioritizes:

1. Official and primary sources
2. Recent sources
3. Sources that directly support the answer

### 6. Final Response

The assistant returns the final answer along with the selected sources.

## Research Controls

The agent has a maximum of **5 tool calls per research request**.

This prevents uncontrolled tool usage and helps keep execution predictable.

The system prompt also contains research-stopping rules to prevent unnecessary searches.

## Installation

Clone the repository:

```bash
git clone <your-repository-url>
cd ai-research-agent
```

Create a virtual environment:

```bash
python -m venv venv
```

Activate it on Windows:

```powershell
venv\Scripts\activate
```

Install dependencies:

```bash
pip install -r requirements.txt
```

## Environment Variables

Create a `.env` file:

```text
GOOGLE_API_KEY=your_google_api_key_here
```

Never commit `.env` to Git.

## Running the Streamlit App

```bash
streamlit run app.py
```

The application will open in your browser.

## Running the CLI

```bash
python main.py
```

Then enter your research question.

## Example Questions

### Current Information

```text
What is the latest stable version of Python?
```

### Official Source Verification

```text
What are the current system requirements for Windows 11?
Find the official Microsoft source.
```

### Calculation

```text
What is the compound annual growth rate if an investment
grows from $10,000 to $18,000 in 5 years?
```

### Webpage Analysis

```text
Read the official Python release page and explain the
important changes in the latest release.
```

## Technologies

* Python
* LangChain
* Google Gemini
* Streamlit
* python-dotenv

## Project Status

**Version 1.0 — Complete**

The current version includes:

* Agentic tool calling
* Web research
* Webpage analysis
* Mathematical calculations
* Source tracking
* AI source selection
* Research stopping rules
* Tool-call limits
* Streamlit interface
* CLI interface

## Future Improvements

Possible future versions could include:

* Conversation history
* Streaming responses
* Persistent research sessions
* Improved source ranking
* Parallel web searches
* Research summaries
* Export to PDF/Markdown
* More specialized research tools
* Deployment as a public web application

## License

This project is intended as a portfolio and learning project.
