# RAG Intelligence Agent

A sophisticated Retrieval-Augmented Generation (RAG) intelligence agent built with LangGraph, enabling intelligent document indexing, retrieval, and context-aware response generation. This template provides a foundation for building enterprise-grade RAG systems with multi-graph architecture supporting complex research and analysis workflows.

## Table of Contents

- [Description](#description)
- [Tech Stack](#tech-stack)
- [Features](#features)
- [Project Structure](#project-structure)
- [Installation](#installation)
- [Usage](#usage)
- [Configuration](#configuration)
- [Dependencies](#dependencies)
- [Contribution Guide](#contribution-guide)
- [Deployment](#deployment)
- [Troubleshooting](#troubleshooting)
- [Security](#security)
- [License](#license)

## Description

The RAG Intelligence Agent is a comprehensive starter template designed to help developers build sophisticated retrieval-augmented generation systems using LangGraph and LangGraph Studio. It features a modular architecture with three main graph components:

1. **Index Graph** - Manages document indexing and storage into vector databases
2. **Retrieval Graph** - Handles conversational interactions with query routing and response generation
3. **Researcher Subgraph** - Conducts multi-step research by generating and executing search queries

The system is designed to work with various LLM providers (Anthropic, OpenAI, Fireworks) and multiple vector store backends (Elasticsearch, MongoDB, Pinecone), making it highly flexible and scalable for diverse deployment scenarios.

### Key Capabilities

- **Multi-step Research**: Automatically creates and executes research plans based on user queries
- **Smart Query Routing**: Classifies incoming queries and routes them to appropriate handlers
- **Conversational Context**: Maintains chat history for coherent multi-turn conversations
- **Flexible Backends**: Supports multiple LLM and vector store providers
- **Graph-based Workflow**: Leverages LangGraph for stateful, multi-actor applications
- **Studio Integration**: Full compatibility with LangGraph Studio for visual graph development and debugging

## Tech Stack

### Core Framework
- **LangGraph** (>= 0.2.6) - Graph-based orchestration for AI workflows
- **LangChain** (>= 0.2.14) - Building blocks for LLM applications
- **LangChain OpenAI** (>= 0.1.22) - OpenAI integration
- **LangChain Anthropic** (>= 0.1.23) - Anthropic Claude integration
- **LangChain Fireworks** (>= 0.1.7) - Fireworks AI integration

### Vector Stores & Retrieval
- **LangChain Elasticsearch** (>= 0.2.2, < 0.3.0) - Elastic vector search
- **LangChain MongoDB** (>= 0.1.9) - MongoDB Atlas integration
- **LangChain Pinecone** (>= 0.1.3, < 0.2.0) - Pinecone serverless
- **LangChain Cohere** (>= 0.2.4) - Cohere embeddings

### Utilities
- **Python-dotenv** (>= 1.0.1) - Environment variable management
- **msgspec** (>= 0.18.6) - Fast serialization

### Development Tools
- **mypy** (>= 1.11.1) - Static type checking
- **ruff** (>= 0.6.1) - Fast Python linter and formatter
- **pytest** - Testing framework
- **pytest-watch** - Test automation

## Features

### Intelligent Query Processing

- **Query Classification**: Analyzes user queries to determine routing:
  - LangChain-specific queries trigger research plans
  - Ambiguous queries prompt for clarification
  - General queries receive direct responses

- **Dynamic Research Plans**: For LangChain queries, generates step-by-step research plans that break down complex questions into manageable research steps

### Multi-Provider Support

**Language Models:**
- Anthropic Claude (1.2, 2.0, 2.1, 3-opus, 3-sonnet, 3.5-sonnet, 3-haiku)
- OpenAI GPT (3.5-turbo, 4, 4-turbo, 4o, 4o-mini)
- Fireworks AI models

**Embedding Models:**
- OpenAI text-embedding (ada-002, 3-small, 3-large)
- Cohere embeddings (multiple variants for different languages)

**Vector Stores:**
- Elasticsearch (local, Elastic Cloud, serverless)
- MongoDB Atlas Vector Search
- Pinecone Serverless
- Local Elasticsearch with Docker

### Conversational Intelligence

- **Chat History Management**: Maintains full conversation context
- **Multi-turn Interactions**: Handles follow-up questions with awareness of previous context
- **Document-aware Responses**: Generates responses based on retrieved documents
- **Flexible Prompting**: Customizable system prompts for different use cases

### Developer Experience

- **Visual Graph Development**: Edit graphs in LangGraph Studio
- **Hot Reload**: Auto-apply local changes during development
- **State Inspection**: Debug by editing past state and re-running
- **LangSmith Integration**: Built-in tracing and monitoring

## Project Structure

```
rag-intelligence-agent/
├── src/
│   ├── index_graph/
│   │   ├── __init__.py
│   │   ├── graph.py              # Index graph definition
│   │   ├── state.py              # State definitions
│   │   └── configuration.py       # Configuration schema
│   ├── retrieval_graph/
│   │   ├── __init__.py
│   │   ├── graph.py              # Main retrieval graph
│   │   ├── state.py              # State definitions
│   │   ├── configuration.py       # Configuration schema
│   │   ├── prompts.py            # System and user prompts
│   │   └── researcher_graph/
│   │       ├── __init__.py
│   │       ├── graph.py          # Researcher subgraph
│   │       └── state.py          # Researcher state
│   └── shared/
│       ├── __init__.py
│       ├── configuration.py       # Shared configurations
│       ├── state.py              # Shared state types
│       ├── retrieval.py          # Retrieval implementations
│       └── utils.py              # Utility functions
├── tests/
│   ├── unit_tests/
│   │   ├── __init__.py
│   │   └── test_configuration.py
│   └── integration_tests/
│       ├── __init__.py
│       └── test_graph.py
├── static/
│   └── studio_ui.png             # UI screenshots
├── .github/
│   └── workflows/
│       ├── unit-tests.yml        # CI/CD for unit tests
│       └── integration-tests.yml # CI/CD for integration tests
├── .env.example                  # Environment template
├── .gitignore
├── .codespellignore
├── langgraph.json               # LangGraph Studio config
├── Makefile                      # Development commands
├── pyproject.toml               # Project metadata
├── LICENSE                       # MIT License
└── README.md                     # This file
```

### Key Files

| File | Purpose |
|------|---------|
| `src/index_graph/graph.py` | Handles document indexing into vector stores |
| `src/retrieval_graph/graph.py` | Main graph orchestrating query routing and responses |
| `src/retrieval_graph/researcher_graph/graph.py` | Subgraph for multi-step research execution |
| `src/shared/retrieval.py` | Vector store initialization and retrieval logic |
| `src/shared/utils.py` | Utility functions (model loading, document formatting) |
| `langgraph.json` | Specifies graphs available in LangGraph Studio |

## Installation

### Prerequisites

- Python 3.9 or higher
- pip or [uv](https://astral.sh/uv/) package manager
- Access to at least one LLM API (Anthropic, OpenAI, or Fireworks)
- Access to at least one vector store (Elasticsearch, MongoDB, or Pinecone)

### Setup Steps

1. **Clone the repository**

```bash
git clone https://github.com/Tanushh18/rag-intelligence-agent.git
cd rag-intelligence-agent
```

2. **Create a Python virtual environment**

```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. **Install dependencies**

```bash
# Using pip
pip install -e ".[dev]"

# Or using uv (faster)
uv pip install -e ".[dev]"
```

4. **Configure environment variables**

```bash
cp .env.example .env
```

Edit `.env` with your API keys and configuration (see [Configuration](#configuration) section).

5. **Install LangGraph Studio** (optional, for visual development)

Download from [LangGraph Studio](https://github.com/langchain-ai/langgraph-studio)

## Usage

### Basic Workflow

#### 1. Index Documents

Open LangGraph Studio or use the Python API to invoke the indexer:

```python
from index_graph import graph as indexer

# Index with default sample documents
result = await indexer.ainvoke({
    "docs": [],  # Empty uses sample docs from LangChain documentation
})

# Or index with custom documents
custom_docs = [
    {"page_content": "Your document content here"},
    {"page_content": "Another document"}
]
result = await indexer.ainvoke({"docs": custom_docs})
```

#### 2. Query Documents

Use the retrieval graph for conversational interactions:

```python
from retrieval_graph import graph as retrieval

# Single query
response = await retrieval.ainvoke({
    "messages": [
        {"role": "user", "content": "What is LangGraph?"}
    ]
})

# Multi-turn conversation
messages = [
    {"role": "user", "content": "What is LangGraph?"},
    {"role": "assistant", "content": "LangGraph is..."},
    {"role": "user", "content": "How does it compare to LangChain?"}
]
response = await retrieval.ainvoke({"messages": messages})
```

### LangGraph Studio Workflow

1. Open LangGraph Studio
2. Select "indexer" from dropdown → invoke with empty input to load sample documents
3. Switch to "retrieval_graph" → ask questions about LangChain/LangGraph
4. Use the visual interface to:
   - Edit state at checkpoints
   - Re-run from previous states for debugging
   - Modify prompts in real-time
   - View streaming responses

### Making Development Changes

Local changes are automatically applied via hot reload:

1. Modify graph definitions or prompts
2. See changes reflected immediately in Studio
3. Create new threads with `+` button to test variations
4. Use LangSmith integration for production tracing

## Configuration

Configuration is managed through environment variables and configuration classes. Each graph has a `Configuration` class in `configuration.py`.

### Environment Variables

Create `.env` file (copy from `.env.example`):

```bash
# LangSmith (optional, for tracing)
LANGSMITH_PROJECT=rag-research-agent

# LLM Selection - Choose at least one
ANTHROPIC_API_KEY=your-key-here
OPENAI_API_KEY=your-key-here
FIREWORKS_API_KEY=your-key-here
```

### Vector Store Configuration

#### Elasticsearch

**Elasticsearch Serverless (14-day free trial):**

```bash
# Sign up: https://cloud.elastic.co/
ELASTICSEARCH_URL=<your-serverless-url>
ELASTICSEARCH_API_KEY=<your-api-key>
```

**Elastic Cloud:**

```bash
ELASTICSEARCH_URL=<your-cloud-url>
ELASTICSEARCH_API_KEY=<your-api-key>
```

**Local Docker:**

```bash
docker run \
  -p 127.0.0.1:9200:9200 \
  -d \
  --name elasticsearch \
  -e ELASTIC_PASSWORD=changeme \
  -e "discovery.type=single-node" \
  -e "xpack.security.http.ssl.enabled=false" \
  -e "xpack.license.self_generated.type=trial" \
  docker.elastic.co/elasticsearch/elasticsearch:8.15.1

# In .env:
ELASTICSEARCH_URL=http://host.docker.internal:9200
ELASTICSEARCH_USER=elastic
ELASTICSEARCH_PASSWORD=changeme
```

#### MongoDB Atlas

1. Create free account at https://www.mongodb.com/cloud/atlas
2. Create cluster and database
3. Create vector search index on `langgraph_retrieval_agent.default` collection
4. Get connection string from Atlas dashboard

```bash
MONGODB_URI=mongodb+srv://user:password@cluster.mongodb.net/?retryWrites=true&w=majority
```

#### Pinecone Serverless

1. Sign up at https://login.pinecone.io/
2. Create serverless index (1536 dimensions for OpenAI embeddings)
3. Generate API key

```bash
PINECONE_API_KEY=your-api-key
PINECONE_INDEX_NAME=your-index-name
```

### Model Configuration

In LangGraph Studio, configure these parameters:

| Parameter | Default | Options |
|-----------|---------|---------|
| `response_model` | anthropic/claude-3-5-sonnet-20240620 | Claude, GPT-4, GPT-4o variants |
| `query_model` | anthropic/claude-3-haiku-20240307 | Claude, GPT-3.5-turbo, GPT-4 variants |
| `embedding_model` | openai/text-embedding-3-small | OpenAI, Cohere embeddings |
| `retriever_provider` | elastic-local | elastic, elastic-local, mongodb, pinecone |

### Customization Options

1. **Change Retriever**: Switch `retriever_provider` between providers
2. **Modify Embedding Model**: Update `embedding_model` in configuration
3. **Adjust Search Parameters**: Modify `search_kwargs` for retrieval behavior
4. **Customize Responses**: Edit `response_system_prompt`
5. **Update Prompts**: Modify prompts in `src/retrieval_graph/prompts.py`:
   - `research_plan_system_prompt` - For research planning
   - `generate_queries_system_prompt` - For query generation
6. **Change LLM**: Update `response_model` and `query_model`
7. **Extend Graph**: Add nodes/edges in `src/retrieval_graph/graph.py`
8. **Add Tools**: Implement new tools in researcher graph

## Dependencies

### Core Dependencies

| Package | Version | Purpose |
|---------|---------|---------|
| langgraph | >= 0.2.6 | Graph-based AI orchestration |
| langchain | >= 0.2.14 | LLM framework |
| langchain-openai | >= 0.1.22 | OpenAI integration |
| langchain-anthropic | >= 0.1.23 | Anthropic Claude integration |
| langchain-fireworks | >= 0.1.7 | Fireworks AI integration |
| python-dotenv | >= 1.0.1 | Environment management |
| msgspec | >= 0.18.6 | Serialization |

### Vector Store Adapters

| Package | Version | Vector Store |
|---------|---------|--------------|
| langchain-elasticsearch | 0.2.2 - 0.3.0 | Elasticsearch |
| langchain-mongodb | >= 0.1.9 | MongoDB Atlas |
| langchain-pinecone | 0.1.3 - 0.2.0 | Pinecone |
| langchain-cohere | >= 0.2.4 | Cohere embeddings |

### Development Dependencies

| Package | Version | Purpose |
|---------|---------|---------|
| mypy | >= 1.11.1 | Static type checking |
| ruff | >= 0.6.1 | Linting & formatting |
| pytest | Latest | Testing |
| pytest-watch | Latest | Test automation |

## Contribution Guide

### Development Setup

```bash
# Create fork and clone
git clone https://github.com/YOUR-USERNAME/rag-intelligence-agent.git
cd rag-intelligence-agent

# Create virtual environment
python -m venv venv
source venv/bin/activate

# Install with dev dependencies
pip install -e ".[dev]"
```

### Code Standards

- **Format Code**: `make format`
- **Run Linting**: `make lint`
- **Type Checking**: mypy (strict mode enforced)
- **Spell Check**: `make spell_check`

### Testing

```bash
# Run unit tests
make test

# Run specific test file
make test TEST_FILE=tests/unit_tests/test_configuration.py

# Watch mode (auto-rerun on changes)
make test_watch

# Integration tests
make integration_tests

# Coverage profiling
make test_profile
```

### Commit Guidelines

1. Create feature branch: `git checkout -b feature/description`
2. Make changes and test thoroughly
3. Format and lint: `make format lint`
4. Commit with descriptive message
5. Push to fork: `git push origin feature/description`
6. Create pull request with:
   - Clear title and description
   - Reference to related issues
   - Explanation of changes

### Pull Request Process

1. Ensure all tests pass locally
2. Update documentation if needed
3. Add tests for new functionality
4. Ensure code is properly formatted
5. Request review from maintainers

## Deployment

### Local Development

```bash
# Using LangGraph Studio (recommended)
# - Open Studio
# - Load project: Open in - LangGraph Studio

# Using Python directly
python -c "
from retrieval_graph import graph as retrieval
import asyncio

async def main():
    response = await retrieval.ainvoke({
        'messages': [{'role': 'user', 'content': 'What is LangGraph?'}]
    })
    print(response)

asyncio.run(main())
"
```

### Docker Deployment

For containerized deployment with dependencies:

```dockerfile
FROM python:3.11-slim

WORKDIR /app

# Copy project
COPY . .

# Install dependencies
RUN pip install -e .

# Set environment (from mounted secrets)
ENV PYTHONUNBUFFERED=1

# Run with your orchestration tool
CMD ["python", "-c", "...your-invocation..."]
```

### Cloud Deployment

**LangGraph Cloud** (Recommended):

1. Push code to GitHub
2. Link repository to LangGraph Cloud
3. Set environment variables in Cloud console
4. Deploy with one click

**Other Platforms** (AWS, GCP, Azure):

1. Use Docker deployment approach
2. Configure environment secrets
3. Set up API gateway/load balancer
4. Configure monitoring and logging

### Production Checklist

- [ ] All environment variables set securely
- [ ] Vector database sized appropriately
- [ ] LLM rate limits configured
- [ ] LangSmith tracing enabled for monitoring
- [ ] Logging configured for debugging
- [ ] Error handling and retries implemented
- [ ] Load testing completed
- [ ] Backup strategy for indexed documents

## Troubleshooting

### Common Issues

#### 1. API Key Errors

**Problem**: `AuthenticationError` or `Invalid API key`

**Solution**:
```bash
# Verify .env file exists and has correct keys
cat .env

# Check key format (no extra spaces or quotes)
export ANTHROPIC_API_KEY="your-key-here"

# Test connection
python -c "from langchain_anthropic import ChatAnthropic; ChatAnthropic()"
```

#### 2. Vector Store Connection Failures

**Problem**: `ConnectionError` to Elasticsearch/MongoDB/Pinecone

**Solution**:
```bash
# Check service is running
# For Elasticsearch Docker:
docker ps | grep elasticsearch

# Verify connection string in .env
# Test directly:
curl http://localhost:9200  # Elasticsearch
```

#### 3. Module Import Errors

**Problem**: `ModuleNotFoundError: No module named 'retrieval_graph'`

**Solution**:
```bash
# Install in editable mode
pip install -e .

# Verify PYTHONPATH
export PYTHONPATH=/path/to/src:$PYTHONPATH
```

#### 4. Graph Execution Timeouts

**Problem**: Queries take too long to complete

**Solution**:
- Increase retrieval result count
- Use faster embedding model (ada-002 → 3-small)
- Check vector store performance
- Review LangSmith traces for bottlenecks

#### 5. Memory Issues with Large Documents

**Problem**: OutOfMemory errors during indexing

**Solution**:
```bash
# Batch indexing
docs_batches = [docs[i:i+100] for i in range(0, len(docs), 100)]
for batch in docs_batches:
    await indexer.ainvoke({"docs": batch})
```

#### 6. LangGraph Studio Connection Issues

**Problem**: Cannot connect to local development server

**Solution**:
```bash
# Ensure Python virtual environment is active
source venv/bin/activate

# Check Python version (3.9+)
python --version

# Reinstall LangGraph
pip install --force-reinstall langgraph
```

### Debug Mode

Enable debug logging:

```python
import logging
logging.basicConfig(level=logging.DEBUG)

# Run your graph
result = await graph.ainvoke(...)
```

### Performance Optimization

1. **Caching**: Use LLM caching for repeated queries
2. **Batch Processing**: Process documents in batches
3. **Model Selection**: Use smaller models for queries (Haiku vs Sonnet)
4. **Vector DB**: Tune search parameters in `search_kwargs`
5. **Monitoring**: Use LangSmith to identify bottlenecks

## Security

### API Key Management

- Never commit `.env` files to version control
- Use environment variables in production
- Rotate API keys regularly
- Use separate keys for development/production

### Data Privacy

- Vector database contains document embeddings only
- Original documents should be stored separately
- Implement access controls on vector database
- Consider data encryption at rest and in transit

### Model Configuration

- Use separate API keys for different environments
- Implement rate limiting
- Monitor for unusual usage patterns
- Log all requests (respecting privacy regulations)

### Dependencies

- Keep dependencies updated: `pip install --upgrade`
- Use pinned versions in production: `pip-compile`
- Monitor security advisories: `safety check`
- Review new dependency licenses

### Best Practices

1. Use service accounts instead of personal API keys
2. Implement request signing and verification
3. Use HTTPS for all communication
4. Implement rate limiting and quotas
5. Regular security audits of prompts
6. Handle sensitive data carefully in prompts
7. Test for prompt injection vulnerabilities
8. Keep audit logs of system usage

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

### MIT License Summary

- You can use this code freely in personal and commercial projects
- You must include the original license and copyright notice
- The code is provided "as-is" without warranty
- The authors are not liable for any issues

## Additional Resources

- **LangGraph Documentation**: https://github.com/langchain-ai/langgraph
- **LangChain Documentation**: https://python.langchain.com/
- **LangGraph Studio**: https://github.com/langchain-ai/langgraph-studio
- **LangSmith Tracing**: https://smith.langchain.com/
- **Elasticsearch Guide**: https://www.elastic.co/guide/
- **MongoDB Atlas Docs**: https://docs.mongodb.com/atlas/
- **Pinecone Docs**: https://docs.pinecone.io/

## Support & Community

- **Issues**: Report bugs on GitHub Issues
- **Discussions**: Ask questions in GitHub Discussions
- **LangChain Community**: https://discord.gg/6adMQxSpJS

## Citation

If you use this template in your research or project, please cite:

```bibtex
@software{rag-intelligence-agent,
  title={RAG Intelligence Agent},
  author={Tanushh18},
  url={https://github.com/Tanushh18/rag-intelligence-agent},
  year={2024},
  license={MIT}
}
```

---

Built with LangGraph and LangChain | Last updated: 2024
