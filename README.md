# UdaPlay - AI Game Research Agent Project

## Project Overview
UdaPlay is an AI-powered research agent for the video game industry. This project is divided into two main parts that will help you build a sophisticated AI agent capable of answering questions about video games using both local knowledge and web searches.

## Project Structure

### Part 1: Offline RAG (Retrieval-Augmented Generation)
In this part, you'll build a Vector Database using ChromaDB to store and retrieve video game information efficiently.

Key tasks:
- Set up ChromaDB as a persistent client
- Create a collection with appropriate embedding functions
- Process and index game data from JSON files
- Each game document contains:
  - Name
  - Platform
  - Genre
  - Publisher
  - Description
  - Year of Release

### Part 2: AI Agent Development
Build an intelligent agent that combines local knowledge with web search capabilities.

The agent will have the following capabilities:
1. Answer questions using internal knowledge (RAG)
2. Search the web when needed
3. Maintain conversation state
4. Return structured outputs
5. Store useful information for future use

Required Tools to Implement:
1. `retrieve_game`: Search the vector database for game information
2. `evaluate_retrieval`: Assess the quality of retrieved results
3. `game_web_search`: Perform web searches for additional information

## Agent Architecture

You will implement a sophisticated agent system with the following components:

### State Machine Workflow
- **EntryPoint**: Initial state for processing user queries
- **Message Preparation**: Formats conversation history and system instructions
- **LLM Processing**: Routes queries through language models with tool access
- **Tool Execution**: Executes tool calls and processes results
- **Termination**: Completes the workflow and returns results

### Memory Management
- **Short-term Memory**: Maintains conversation context across interactions
- **Session Management**: Supports multiple concurrent conversation sessions
- **State Persistence**: Preserves conversation state between queries

### Tool System
The agent will employ three specialized tools:

**`retrieve_game`**: Semantic search tool for the local vector database
- Searches ChromaDB collection using natural language queries
- Returns JSON-formatted game metadata
- Supports configurable result limits

**`evaluate_retrieval`**: LLM-powered relevance assessment
- Uses GPT-3.5 to evaluate if retrieved context is sufficient
- Returns structured JSON with sufficiency assessment
- Enables intelligent fallback to web search when needed

**`game_web_search`**: Web search integration via Tavily API
- Performs web searches when local knowledge is insufficient
- Returns search results with URLs and content snippets
- Fallback mechanism for handling queries outside the local knowledge base

## Requirements

### Environment Setup

**IMPORTANT: You must set up your API keys before running the project.**

#### Step 1: Create a `.env` file
Create a `.env` file in the project root directory with the following API keys:

```bash
# Required API Keys - Replace with your actual keys
OPENAI_API_KEY="your_openai_api_key_here"
CHROMA_OPENAI_API_KEY="your_openai_api_key_here"  # Can be same as OPENAI_API_KEY
TAVILY_API_KEY="your_tavily_api_key_here"
```

#### Step 2: Obtain API Keys

**OpenAI API Key:**
1. Visit [OpenAI Platform](https://platform.openai.com/)
2. Sign up or log in to your account
3. Navigate to API Keys section
4. Create a new API key
5. Copy the key (starts with `sk-` or `voc-` for Vocareum)

**Tavily API Key:**
1. Visit [Tavily](https://tavily.com/)
2. Sign up for a free account
3. Get your API key from the dashboard
4. Copy the key (starts with `tvly-`)

#### Step 3: Verify Setup
After creating your `.env` file, open the notebooks to test your setup. The notebooks will guide you through verifying your API keys and setting up the required components.

#### ⚠️ Security Notes:
- Never commit your `.env` file to version control
- Keep your API keys secure and don't share them
- The `.env` file is already included in `.gitignore`
- If you encounter authentication errors, verify your API keys are valid and have sufficient credits

### Project Dependencies
- Python 3.11+
- ChromaDB (vector database)
- OpenAI (language model API)
- Tavily (web search API)
- Python-dotenv (environment variables)
- Additional dependencies listed in requirements.txt

### Directory Structure
```
udaplay-ai-agent/
├── chromadb/           # Vector database storage (auto-created)
├── games/              # JSON files with game data (15 games)
├── lib/                # Custom library implementations
│   ├── __init__.py
│   ├── agents.py       # Agent implementations
│   ├── documents.py    # Document processing utilities
│   ├── evaluation.py   # Evaluation utilities
│   ├── llm.py         # LLM abstractions
│   ├── loaders.py     # Data loading utilities
│   ├── memory.py      # Memory management
│   ├── messages.py    # Message handling
│   ├── parsers.py     # Data parsing utilities
│   ├── rag.py         # RAG implementation
│   ├── state_machine.py # State machine framework
│   ├── tooling.py     # Tool implementations
│   └── vector_db.py   # Vector database utilities
├── .env               # API keys configuration (create this)
├── .gitignore         # Git ignore file
├── CODEOWNERS         # Project maintainers
├── LICENSE.md         # MIT license
├── README.md          # This file
├── requirements.txt   # Python dependencies
├── Udaplay_01_starter_project.ipynb  # Part 1: Vector Database
└── Udaplay_02_starter_project.ipynb  # Part 2: AI Agent
```

## Getting Started

### 1. Environment Setup

#### Create and Activate Virtual Environment
```bash
# Create virtual environment
python3 -m venv udaplay-env

# Activate virtual environment
# On macOS/Linux:
source udaplay-env/bin/activate
# On Windows:
udaplay-env\Scripts\activate
```

#### Install Dependencies
```bash
pip install -r requirements.txt
```

### 2. API Configuration

Create a `.env` file in the project root with your API keys:
```bash
# Required API Keys - Replace with your actual keys
OPENAI_API_KEY="your_openai_api_key_here"
CHROMA_OPENAI_API_KEY="your_openai_api_key_here"  # Can be same as OPENAI_API_KEY
TAVILY_API_KEY="your_tavily_api_key_here"
```

### 3. Run the Notebooks

Start with Part 1, then proceed to Part 2:

```bash
# Start Jupyter
jupyter notebook

# Open and complete in order:
# 1. Udaplay_01_starter_project.ipynb
# 2. Udaplay_02_starter_project.ipynb
```

## Working with the Notebooks

### Part 1: Vector Database Setup (Udaplay_01_starter_project.ipynb)
This notebook guides you through:
- Setting up ChromaDB as a persistent client
- Creating a collection with embedding functions
- Processing and indexing the 15 game JSON files
- Testing semantic search functionality

### Part 2: AI Agent Development (Udaplay_02_starter_project.ipynb)
This notebook helps you build:
- A complete AI agent with tool integration
- State machine workflow management
- Memory and session handling
- Tool implementations for game retrieval, evaluation, and web search

## Testing Your Implementation

After completing both notebooks, test your agent with questions like:
- "When was Pokémon Gold and Silver released?"
- "Which one was the first 3D platformer Mario game?"
- "Was Mortal Kombat X released for PlayStation 5?"

## Expected Workflow

1. **Setup**: Install dependencies and configure API keys
2. **Part 1**: Complete the vector database notebook to set up game knowledge retrieval
3. **Part 2**: Build the complete AI agent with tools and memory
4. **Testing**: Verify your agent can handle various gaming queries

## Advanced Features

After completing the basic implementation, you can enhance your agent with:
- Long-term memory capabilities
- Additional tools and capabilities
- Enhanced conversation management

## Notes
- Make sure to implement proper error handling
- Follow best practices for API key management
- Document your code thoroughly
- Test your implementation with various types of queries
