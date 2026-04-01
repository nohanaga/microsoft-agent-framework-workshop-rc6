# Microsoft Agent Framework Workshop

[Microsoft Agent Framework](https://github.com/microsoft/agent-framework) を使って AI エージェントの基礎から高度なマルチエージェントワークフローまでをハンズオン形式で学ぶワークショップです。

## 概要

このワークショップでは、10 本の Jupyter Notebook チュートリアルを通じて、以下の内容を段階的に習得します：

- 単一エージェントへのツール統合
- マルチターン会話とステート管理
- コンテキスト・メモリによるパーソナライゼーション
- Middleware / Filters による本番対応
- マルチエージェントの各種ワークフローパターン
- Human-in-the-Loop（人間参加型）ワークフロー
- エンタープライズ向け MCP 認証

> **Note:** このワークショップは `agent-framework==1.0.0rc6` に最適化されています。異なるバージョンでは API の変更により動作しない場合があります。

## 前提条件

- **Python** 3.11 以上
- **Azure サブスクリプション**（Azure OpenAI Service または Microsoft Foundry へのアクセス）
- **gpt-4.1-mini** モデルなどのデプロイ（Microsoft Foundry 経由）
- **Docker**（Jaeger トレーシングを使用する場合、オプション）

## クイックスタート

```bash
# 1. リポジトリをクローン
git clone https://github.com/nohanaga/microsoft-agent-framework-workshop.git
cd microsoft-agent-framework-workshop

# 2. 依存関係をインストール
pip install -r requirements.txt

# 3. 環境変数を設定（.env ファイルを作成）
# AZURE_OPENAI_ENDPOINT, AZURE_OPENAI_API_KEY, AZURE_OPENAI_CHAT_DEPLOYMENT などを設定

# 4. 最初のチュートリアルを開始
# VS Code で 01_agent_with_tools.ipynb を開いて実行
```

GitHub Codespaces を使用する場合は [SETUP_Codespaces.md](SETUP_Codespaces.md) を参照してください。

## チュートリアル一覧

### 基礎編（01–04）

| # | ノートブック | 内容 |
|---|---|---|
| 01 | [ツールを持つエージェント](01_agent_with_tools.ipynb) | Python 関数をツールとして定義し、エージェントに天気取得・通貨換算などの外部機能を持たせる |
| 02 | [マルチターン会話（Azure OpenAI 版）](02_multi_turn_conversations_openai.ipynb) | `AgentThread` を使った会話コンテキスト維持と OpenTelemetry トレーシング |
| 02b | [マルチターン会話（Foundry Agent Service 版）](02b_multi_turn_conversations_foundry.ipynb) | チュートリアル 02 を Microsoft Foundry Agent Service で実装する代替版 |
| 03 | [コンテキストとメモリ](03_context_and_memory.ipynb) | `ContextProvider` でセッション横断的にユーザーの好みを記憶するパーソナライズドエージェント |
| 04 | [Middleware と Filters](04_middleware_and_filters.ipynb) | リクエスト/レスポンス変換、認証、レート制限、コンテンツフィルタリングなどの本番対応機能 |

### マルチエージェント編（05–09）

| # | ノートブック | 内容 |
|---|---|---|
| 05 | [マルチエージェントワークフロー（基礎）](05_multi_agent_workflows.ipynb) | `SequentialBuilder`（順次）と `ConcurrentBuilder`（並行）によるワークフロー構築 |
| 06 | [協調型マルチエージェント（RoundRobin）](06_collaborative_multi_agent_round_robin.ipynb) | `GroupChatBuilder` を使ったラウンドロビン方式の協調型マルチエージェント + MCP 統合 |
| 07 | [Handoff パターン](07_handoff_multi_domain_agent.ipynb) | `HandoffBuilder` によるドメイン特化エージェントへの委譲（カスタマーサポートシナリオ） |
| 08 | [高度なワークフロー](08_advanced_workflows.ipynb) | `WorkflowBuilder`（カスタム DAG）と `MagenticBuilder`（AI 駆動の動的オーケストレーション） |
| 09 | [Human-in-the-Loop](09_human_in_the_loop.ipynb) | 承認ゲート、インタラクティブリファインメント、条件付き/予算ベース承認パターン |

### エンタープライズ編（10）

| # | ノートブック | 内容 |
|---|---|---|
| 10 | [Foundry MCP 認証](10_foundry_mcp_authentication.ipynb) | Foundry エージェント × MCP サーバーの4つの認証パターン（Unauth / Key / Agentic ID / OAuth） |

## プロジェクト構成

```
microsoft-agent-framework-workshop/
├── 01_agent_with_tools.ipynb              # チュートリアル 01–10
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
│   └── mock_server.py                     # Xbox Game Shop + CRM モック MCP サーバー
├── jaeger/
│   └── docker-compose.yml                 # Jaeger トレーシング環境
├── requirements.txt                       # Python 依存関係
├── SETUP_Codespaces.md                    # GitHub Codespaces セットアップガイド
└── README.md                              # このファイル
```

## MCP サーバー

`mcp/mock_server.py` は **Xbox Game Shop + CRM Social Mock API** を提供するモック MCP（Model Context Protocol）サーバーです。商品、注文、在庫、ユーザー、ソーシャル分析などのサンプルデータが組み込まれています。

チュートリアル 06, 08 で使用します。起動方法：

```bash
python mcp/mock_server.py
```

## トレーシング（Jaeger）

OpenTelemetry によるトレーシングが組み込まれています。チュートリアル 02 以降で利用可能です。

```bash
cd jaeger
docker compose up -d
# http://localhost:16686 で Jaeger UI にアクセス
```

## 環境変数

`.env` ファイルをプロジェクトルートに作成してください：

```bash
AZURE_OPENAI_ENDPOINT="https://your-endpoint.openai.azure.com"
AZURE_OPENAI_API_KEY="your-api-key"
AZURE_OPENAI_CHAT_DEPLOYMENT="gpt-4.1-mini"
AZURE_OPENAI_API_VERSION="2025-03-01-preview"
```

## 使用技術

- [Microsoft Agent Framework](https://github.com/microsoft/agent-framework) — エージェント構築フレームワーク
- [Azure OpenAI Service](https://learn.microsoft.com/azure/ai-services/openai/) — LLM バックエンド
- [Microsoft Foundry](https://ai.azure.com/) — AI プロジェクト管理・エージェントサービス
- [Model Context Protocol (MCP)](https://modelcontextprotocol.io/) — ツール統合プロトコル
- [OpenTelemetry](https://opentelemetry.io/) + [Jaeger](https://www.jaegertracing.io/) — 分散トレーシング

## 謝辞

このワークショップは [Goutham Koneru (@gokoner)](https://github.com/gokoner) 氏のオリジナルリポジトリ [microsoft-agent-framework-workshop](https://github.com/gokoner/microsoft-agent-framework-workshop) に多大なインスピレーションを受けました。充実したチュートリアル群を公開してくださった同氏に深く感謝いたします。

## ライセンス

このプロジェクトは [MIT License](LICENSE) の下で公開されています。
