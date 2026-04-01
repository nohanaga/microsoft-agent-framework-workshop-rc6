# Microsoft Agent Framework Workshop

A hands-on workshop for learning everything from the basics of AI agents to advanced multi-agent workflows using [Microsoft Agent Framework](https://github.com/microsoft/agent-framework).

## Overview

This workshop provides 10 Jupyter Notebook tutorials that progressively cover the following topics:

- Tool integration with a single agent
- Multi-turn conversations and state management
- Personalization through context and memory
- Production-readiness with Middleware / Filters
- Various multi-agent workflow patterns
- Human-in-the-Loop workflows
- Enterprise MCP authentication

> **Note:** This workshop is optimized for `agent-framework==1.0.0rc6`. Different versions may not work due to API changes.

## Prerequisites

- **Python** 3.11 or later
- **Azure subscription** (with access to Azure OpenAI Service or Microsoft Foundry)
- **gpt-4.1-mini** or similar model deployment (via Microsoft Foundry)
- **Docker** (optional, required for Jaeger tracing)

## Quick Start

```bash
# 1. Clone the repository
git clone https://github.com/nohanaga/microsoft-agent-framework-workshop.git
cd microsoft-agent-framework-workshop

# 2. Install dependencies
pip install -r requirements.txt

# 3. Set environment variables (create a .env file)
# Configure AZURE_OPENAI_ENDPOINT, AZURE_OPENAI_API_KEY, AZURE_OPENAI_CHAT_DEPLOYMENT, etc.

# 4. Start the first tutorial
# Open 01_agent_with_tools.ipynb in VS Code and run it
```

If using GitHub Codespaces, refer to [SETUP_Codespaces.md](SETUP_Codespaces.md).

## Tutorial List

### Fundamentals (01–04)

| # | Notebook | Description |
|---|---|---|
| 01 | [Agent with Tools](01_agent_with_tools.ipynb) | Define Python functions as tools and equip the agent with external capabilities such as weather retrieval and currency conversion |
| 02 | [Multi-turn Conversations (Azure OpenAI)](02_multi_turn_conversations_openai.ipynb) | Maintain conversation context using `AgentThread` and OpenTelemetry tracing |
| 02b | [Multi-turn Conversations (Foundry Agent Service)](02b_multi_turn_conversations_foundry.ipynb) | An alternative implementation of Tutorial 02 using Microsoft Foundry Agent Service |
| 03 | [Context and Memory](03_context_and_memory.ipynb) | Build a personalized agent that remembers user preferences across sessions using `ContextProvider` |
| 04 | [Middleware and Filters](04_middleware_and_filters.ipynb) | Production-ready features including request/response transformation, authentication, rate limiting, and content filtering |

### Multi-Agent (05–09)

| # | Notebook | Description |
|---|---|---|
| 05 | [Multi-Agent Workflows (Basics)](05_multi_agent_workflows.ipynb) | Build workflows using `SequentialBuilder` (sequential) and `ConcurrentBuilder` (parallel) |
| 06 | [Collaborative Multi-Agent (RoundRobin)](06_collaborative_multi_agent_round_robin.ipynb) | Round-robin collaborative multi-agent using `GroupChatBuilder` + MCP integration |
| 07 | [Handoff Pattern](07_handoff_multi_domain_agent.ipynb) | Delegation to domain-specific agents using `HandoffBuilder` (customer support scenario) |
| 08 | [Advanced Workflows](08_advanced_workflows.ipynb) | `WorkflowBuilder` (custom DAG) and `MagenticBuilder` (AI-driven dynamic orchestration) |
| 09 | [Human-in-the-Loop](09_human_in_the_loop.ipynb) | Approval gates, interactive refinement, conditional/budget-based approval patterns |

### Enterprise (10)

| # | Notebook | Description |
|---|---|---|
| 10 | [Foundry MCP Authentication](10_foundry_mcp_authentication.ipynb) | Four authentication patterns for Foundry Agent × MCP Server (Unauth / Key / Agentic ID / OAuth) |

## Project Structure

```
microsoft-agent-framework-workshop/
├── 01_agent_with_tools.ipynb              # Tutorials 01–10
├── 02_multi_turn_conversations_openai.ipynb
├── 02b_multi_turn_conversations_foundry.ipynb
├── 03_context_and_memory.ipynb
├── 04_middleware_and_filters.ipynb
├── 05_multi_agent_workflows.ipynb
├── 06_collaborative_multi_agent_round_robin.ipynb
├── 07_handoff_multi_domain_agent.ipynb
├── 08_advanced_workflows.ipynb
├── 09_human_in_the_loop.ipynb
├── 10_foundry_mcp_authentication.ipynb
├── mcp/
│   └── mock_server.py                     # Xbox Game Shop + CRM Mock MCP Server
├── jaeger/
│   └── docker-compose.yml                 # Jaeger tracing environment
├── requirements.txt                       # Python dependencies
├── SETUP_Codespaces.md                    # GitHub Codespaces setup guide
└── README.md                              # This file
```

## MCP Server

`mcp/mock_server.py` is a mock MCP (Model Context Protocol) server that provides the **Xbox Game Shop + CRM Social Mock API**. It includes built-in sample data for products, orders, inventory, users, and social analytics.

Used in Tutorials 06 and 08. To start:

```bash
python mcp/mock_server.py
```

## Tracing (Jaeger)

OpenTelemetry-based tracing is built in. Available from Tutorial 02 onwards.

```bash
cd jaeger
docker compose up -d
# Access the Jaeger UI at http://localhost:16686
```

## Environment Variables

Create a `.env` file in the project root:

```bash
AZURE_OPENAI_ENDPOINT="https://your-endpoint.openai.azure.com"
AZURE_OPENAI_API_KEY="your-api-key"
AZURE_OPENAI_CHAT_DEPLOYMENT="gpt-4.1-mini"
AZURE_OPENAI_API_VERSION="2025-03-01-preview"
```

## Technologies Used

- [Microsoft Agent Framework](https://github.com/microsoft/agent-framework) — Agent building framework
- [Azure OpenAI Service](https://learn.microsoft.com/azure/ai-services/openai/) — LLM backend
- [Microsoft Foundry](https://ai.azure.com/) — AI project management and agent service
- [Model Context Protocol (MCP)](https://modelcontextprotocol.io/) — Tool integration protocol
- [OpenTelemetry](https://opentelemetry.io/) + [Jaeger](https://www.jaegertracing.io/) — Distributed tracing

## Acknowledgments

This workshop was greatly inspired by the original repository [microsoft-agent-framework-workshop](https://github.com/gokoner/microsoft-agent-framework-workshop) by [Goutham Koneru (@gokoner)](https://github.com/gokoner). We sincerely thank him for publishing such a comprehensive set of tutorials.

## License

This project is licensed under the [MIT License](../LICENSE).
