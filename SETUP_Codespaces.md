# Microsoft Agent Framework Workshop - GitHub Codespaces セットアップガイド

このワークショップでは **Microsoft Agent Framework** を用いて AI エージェントを設計し、実行する方法をステップバイステップで学びます。

## Setup & Installation

### 1. Codespaces を起動

GitHub リポジトリページの緑色の「**<> Code**」ボタンをクリックし、「**Codespaces**」タブから「**Create codespace on main**」ボタンを押下します。

### 2. システムパッケージのインストール

一部のチュートリアル（マルチエージェントワークフローの可視化など）で Graphviz を使用します。devcontainer には含まれていますが、手動セットアップの場合は以下を実行してください：

```bash
sudo apt update && sudo apt install -y graphviz
```

### 3. Python 依存関係のインストール

Codespaces にはすでに Python がインストールされています。Python 3.11.x 以上で動作確認済みです。

```bash
python -V
```

Python のバージョンを確認した後、依存関係をインストールします。

```bash
pip install -r requirements.txt
```

#### 主な依存パッケージ

- `agent-framework` — Microsoft Agent Framework コア
- `agent-framework-azure-ai` — Microsoft Foundry 統合
- `agent-framework-devui` — 開発用 UI
- `agent-framework-mem0` — メモリ統合
- `openai` / `azure-ai-agents` / `azure-identity` — Azure OpenAI & AI サービス
- `fastmcp` / `uvicorn` — MCP サーバー
- `opentelemetry-exporter-otlp-proto-grpc` — トレーシング（OpenTelemetry）
- `pandas` / `numpy` / `matplotlib` — データ処理・可視化

---

### 4. Microsoft Foundry で LLM モデルをデプロイ

1. [ai.azure.com](https://ai.azure.com/) にログインします。アカウントがない場合は新規作成してください。
2. プロジェクトを作成します。既存のハブがない場合は新しいハブを作成します。これにより、ハブ、プロジェクト コンテナ、AI サービス、ストレージ アカウント、および Key Vault が設定されます。
3. API キーと Azure OpenAI Service エンドポイントを取得します（次の手順で `.env` ファイルに設定します）。
4. プロジェクトページで、「**モデル + エンドポイント**」→「**モデルを展開**」→「**ベースモデルを展開**」→「**gpt-4.1**」を選択します。
5. 展開タイプ（Standard、Global Standard など）と地域を選択します。
6. 展開の詳細をカスタマイズし、分あたりのトークン数を 10K に減らし、動的クォータを無効にします。

### 5. 環境変数の設定

`.env` ファイルをプロジェクトルートに作成し、以下の内容を記入してください：

```bash
# Azure OpenAI Service エンドポイント
# 例: https://my-ai-services12345.openai.azure.com/
AZURE_OPENAI_ENDPOINT="https://your-openai-service-endpoint.openai.azure.com"

# Azure OpenAI API キー
AZURE_OPENAI_API_KEY="your-openai-api-key"

# デプロイしたモデル名
AZURE_OPENAI_CHAT_DEPLOYMENT="gpt-4.1-mini"

# API バージョン
AZURE_OPENAI_API_VERSION="2025-03-01-preview"
```

> **Note:** Azure リソースが正しいモデル展開名、エンドポイント、および API バージョンを使用するように構成されていることを確認してください。`.env` ファイルはバージョン管理にコミットしないでください。

---

### 6. MCP サーバーの起動

一部のチュートリアル（06, 08 など）では MCP（Model Context Protocol）サーバーを使用します。ターミナルで以下を実行してください：

```bash
python mcp/mock_server.py
# このターミナルを閉じないでください。ノートブック実行用に別のターミナルを使用します。
```

MCP サーバーは Xbox Game Shop + CRM Social Mock API のモックデータを提供します。

> **Tip:** VS Code タスクを使えばワンクリックで起動できます（下記参照）。

### VS Code タスクによる起動（推奨）

このリポジトリには `.vscode/tasks.json` が含まれており、MCP サーバーをバックグラウンドタスクとして簡単に起動できます。

1. `Ctrl+Shift+P`（macOS: `Cmd+Shift+P`）でコマンドパレットを開きます。
2. 「**Tasks: Run Task**」と入力して選択します。
3. 一覧から「**Run MCP Server**」を選択します。
4. VS Code 下部のターミナルパネルに MCP サーバーのログが表示されれば起動成功です。

> **Note:** タスクは `isBackground: true` で定義されているため、バックグラウンドで実行され続けます。サーバーを停止するには、ターミナルパネルで該当のターミナルを選択し、`Ctrl+C` で終了してください。

---

## Tracing and Observability（オプション）

Microsoft Agent Framework には OpenTelemetry ベースのトレーシングが組み込まれています。チュートリアル 02 以降でトレースの収集・可視化を体験できます。

テレメトリバックエンドとして [Jaeger](https://www.jaegertracing.io/download/) を使用します。Docker Compose で Jaeger をローカルに起動できます。

```bash
cd jaeger
mkdir esdata
# Linux/macOS の場合:
# sudo chown -R 1000:1000 ./esdata
docker compose up -d
```

コピペ用: 
```bash
cd jaeger && mkdir -p esdata && sudo chown -R 1000:1000 esdata && docker compose up -d
```

起動後、[http://localhost:16686](http://localhost:16686) にアクセスして Jaeger UI を確認できます。Codespaces の場合は「**ポート**」タブからポート `16686` の転送アドレスを開いてください。

---

## Jupyter Notebook の設定

1. VS Code のエクスプローラーからいずれかの `.ipynb` ファイル（例: `01_agent_with_tools.ipynb`）を開きます。
2. Notebook 右上の「**カーネルの選択**」をクリックします。
3. 「**Python 環境...**」を選択し、Python 3.11 以上の環境を選択します。
   - Jupyter 拡張が未インストールの場合は、表示される「拡張機能の候補をインストールまたは有効にする Python + Jupyter」をクリックしてインストールします。
4. カーネルが設定されたら、最初のセルを `Shift+Enter` で実行して動作確認を行います。

---

## Notes & Best Practices

- `.env` ファイル内のシークレット（API キーなど）は、バージョン管理にコミットしないでください。
- MCP サーバーを使用するチュートリアルでは、ノートブック実行前にサーバーが起動していることを確認してください。
- Jaeger によるトレーシングはオプションですが、エージェントの実行フローを理解するのに非常に有用です。

---

## Acknowledgments

- [Microsoft Agent Framework](https://github.com/microsoft/agent-framework)
- [Model Context Protocol (MCP)](https://modelcontextprotocol.io/)
- [Microsoft Foundry](https://ai.azure.com/)
