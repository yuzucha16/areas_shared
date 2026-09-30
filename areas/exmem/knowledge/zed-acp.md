---
type: knowledge
title: Zed ACP
status: active
tags:
  - tool/zed
  - acp
  - setup
  - ai/codex
  - ai/claude
aliases:
  - Zed ACP
created: 2026-09-26
updated: 2026-09-26
sources:
  - ChatGPT conversation "Zed ACP ハンズオン" (2026-09-26)
---

# Zed ACP

## Purpose

ZedをAI開発の統合UIとして使い、複数のExternal AgentをACP経由で接続する。

ZedのExternal AgentsはACPを介して別プロセスとして動作し、認証・モデル・課金・ネイティブ設定などは基本的に各Agent側が管理する。ZedはAgent Panel / Threads Sidebarでそれらをホストする。

## Current Agents

バージョンは 2026-09-26 時点。

### Codex

- ACP Registryからインストール
- Version: 1.13.1
- ChatGPT認証を使用
- 最小通信テスト成功

### Claude Agent

- ACP Registryからインストール
- Version: 0.81.2
- Claude Subscription認証を使用
- 最小通信テスト成功

## Setup Steps

1. ZedのACP RegistryからAgentをインストールする。
2. 認証する。
   - Codex: ChatGPT認証
   - Claude Agent: `/login` を実行し、`Claude Subscription` を選ぶ
3. 最小通信テストを送る。

```text
Hello. Reply with exactly: ACP connection OK
```

期待する応答:

```text
ACP connection OK
```

Registryからインストールすると、`settings.json` に次の設定が入る（2026-09-26 に確認）。

```json
"agent_servers": {
  "claude-acp": { "type": "registry" },
  "codex-acp": { "type": "registry" }
}
```

## Setup Pattern

```text
Zed
  |
  +-- ACP --> Codex
  |             |
  |             +-- ChatGPT authentication
  |
  +-- ACP --> Claude Agent
                |
                +-- Claude Subscription authentication
```

## Important Boundary

ACPはAIサービス間の会話履歴同期プロトコルではない。

ACPの役割は、

```text
Editor / Client
      |
     ACP
      |
External Agent
```

というAgent接続。

したがって、ZedのACPセッションをChatGPT通常チャット履歴やClaude通常チャット履歴へ自動同期する仕組みとは考えない。

## Zed Thread History

Zedは設定済みExternal Agentから既存ThreadをImportできる。

これは、

```text
External Agent
      ↓
     ACP
      ↓
Zed Thread History
```

という方向。

## Decisions

### Claude AgentはClaude Subscription認証を使う（2026-09-26）

- 根拠: 定額のClaude契約を使うため。
- 却下案: Anthropic Console（API従量課金）。

## Gotchas

### Codex: `Missing optional dependency @openai/codex-win32-x64`

- 状況: Codex初回起動時に発生。PowerShellからは `node` / `npm` が使えない環境だった。
- 原因の見立て: ZedのACP Registryは自前のNode.js環境でAgentを動かすため、システムにNode.jsがないこと自体は問題ではない。インストールが不完全だった可能性が高い。
- 解決: Codexを再インストールしたら解消した。

### Claude Agent: `/login` が入力候補に出ない

- 状況: `/login` の候補表示に出てこない。
- 解決: `/login` を直接入力して実行すると認証画面が出る。

### Claude Agent: 認証直後の `Session not found`

- 状況: 認証後、最初のThreadで会話を始めると `An Error Happened / Session not found` が出る。
- 解決: `+` から新しいThreadを作ると会話できる。

### 通信ログの確認

ACPの通信ログはZed Command Paletteの `dev: open acp logs` で確認できる。

## Related

- [[ai-development-workflow]]
- [[zed-vim]]

## Reference

- Zed External Agents:
  https://zed.dev/docs/ai/external-agents
- Zed Agent:
  https://zed.dev/docs/ai/agents
- Agent Settings:
  https://zed.dev/docs/ai/agent-settings
