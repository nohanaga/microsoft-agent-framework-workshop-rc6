# Microsoft Agent Framework Workshop - GitHub Codespaces Setup Guide

This workshop teaches you how to design and run AI agents using **Microsoft Agent Framework** in a step-by-step manner.

## Setup & Installation

### 1. Launch Codespaces

Click the green "**<> Code**" button on the GitHub repository page, then select the "**Codespaces**" tab and click "**Create codespace on main**".

### 2. Install System Packages

Some tutorials (such as multi-agent workflow visualization) use Graphviz. It is included in the devcontainer, but for manual setup, run the following:

```bash
sudo apt update && sudo apt install -y graphviz
```

### 3. Install Python Dependencies

Python is already installed in Codespaces. This workshop has been tested with Python 3.11.x and above.

```bash
python -V
```

After checking the Python version, install the dependencies:

```bash
pip install -r requirements.txt
```

#### Key Dependencies

- `agent-framework` — Microsoft Agent Framework core
- `agent-framework-azure-ai` — Microsoft Foundry integration
- `agent-framework-devui` — Development UI
- `agent-framework-mem0` — Memory integration
- `openai` / `azure-ai-agents` / `azure-identity` — Azure OpenAI & AI services
- `fastmcp` / `uvicorn` — MCP server
- `opentelemetry-exporter-otlp-proto-grpc` — Tracing (OpenTelemetry)
- `pandas` / `numpy` / `matplotlib` — Data processing & visualization

---

### 4. Deploy an LLM Model on Microsoft Foundry

1. Log in to [ai.azure.com](https://ai.azure.com/). Create a new account if you don't have one.
2. Create a project. If you don't have an existing hub, create a new one. This will set up a hub, project container, AI services, storage account, and Key Vault.
3. Obtain the API key and Azure OpenAI Service endpoint (you will configure them in the `.env` file in the next step).
4. On the project page, navigate to "**Models + endpoints**" → "**Deploy model**" → "**Deploy base model**" → select "**gpt-4.1**".
5. Choose the deployment type (Standard, Global Standard, etc.) and region.
6. Customize the deployment details, reduce tokens per minute to 10K, and disable dynamic quota.

### 5. Configure Environment Variables

Create a `.env` file in the project root with the following contents:

```bash
# Azure OpenAI Service endpoint
# Example: https://my-ai-services12345.openai.azure.com/
AZURE_OPENAI_ENDPOINT="https://your-openai-service-endpoint.openai.azure.com"

# Azure OpenAI API key
AZURE_OPENAI_API_KEY="your-openai-api-key"

# Deployed model name
AZURE_OPENAI_CHAT_DEPLOYMENT="gpt-4.1-mini"

# API version
AZURE_OPENAI_API_VERSION="2025-03-01-preview"
```

> **Note:** Make sure your Azure resources are configured with the correct model deployment name, endpoint, and API version. Do not commit the `.env` file to version control.

---

### 6. Start the MCP Server

Some tutorials (e.g., 06, 08) use an MCP (Model Context Protocol) server. Run the following in a terminal:

```bash
python mcp/mock_server.py
# Do not close this terminal. Use a separate terminal for running notebooks.
```

The MCP server provides mock data for the Xbox Game Shop + CRM Social Mock API.

> **Tip:** You can start it with a single click using VS Code tasks (see below).

### Starting with VS Code Tasks (Recommended)

This repository includes `.vscode/tasks.json`, which allows you to easily start the MCP server as a background task.

1. Open the Command Palette with `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`).
2. Type "**Tasks: Run Task**" and select it.
3. Choose "**Run MCP Server**" from the list.
4. If the MCP server logs appear in the terminal panel at the bottom of VS Code, the server has started successfully.

> **Note:** The task is defined with `isBackground: true`, so it will continue running in the background. To stop the server, select the corresponding terminal in the terminal panel and press `Ctrl+C`.

---

## Tracing and Observability (Optional)

Microsoft Agent Framework has built-in OpenTelemetry-based tracing. You can experience trace collection and visualization from Tutorial 02 onwards.

[Jaeger](https://www.jaegertracing.io/download/) is used as the telemetry backend. You can start Jaeger locally with Docker Compose:

```bash
cd jaeger
mkdir esdata
# For Linux/macOS:
# sudo chown -R 1000:1000 ./esdata
docker compose up -d
```

Copy-paste version:
```bash
cd jaeger && mkdir -p esdata && sudo chown -R 1000:1000 esdata && docker compose up -d
```

Once started, access the Jaeger UI at [http://localhost:16686](http://localhost:16686). In Codespaces, open the forwarded address for port `16686` from the "**Ports**" tab.

---

## Jupyter Notebook Configuration

1. Open any `.ipynb` file (e.g., `01_agent_with_tools.ipynb`) from the VS Code Explorer.
2. Click "**Select Kernel**" in the top-right corner of the notebook.
3. Select "**Python Environments...**" and choose a Python 3.11+ environment.
   - If the Jupyter extension is not installed, click the prompt to install or enable "Python + Jupyter" extension recommendations.
4. Once the kernel is set, run the first cell with `Shift+Enter` to verify everything works.

---

## Notes & Best Practices

- Do not commit secrets (such as API keys) in the `.env` file to version control.
- For tutorials that use the MCP server, make sure the server is running before executing the notebook.
- Jaeger tracing is optional but very useful for understanding agent execution flows.

---

## Acknowledgments

- [Microsoft Agent Framework](https://github.com/microsoft/agent-framework)
- [Model Context Protocol (MCP)](https://modelcontextprotocol.io/)
- [Microsoft Foundry](https://ai.azure.com/)
