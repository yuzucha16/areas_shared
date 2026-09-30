---
type: project
title: AI開発ワークフロー Project Context
status: active
tags:
  - workflow
  - knowledge-management
aliases:
  - AI開発ワークフロー Project Context
created: 2026-09-26
updated: 2026-09-26
---

# AI開発ワークフロー Project Context

## Current State

- ZedにCodexとClaude AgentをACPで接続済み（[[zed-acp]]）。
- ナレッジ構成を `inbox/` → `knowledge/` → `projects/` の形に整理した。会話ログは常設しない（[[ai-development-workflow]] D2）。
- 各エージェントの入口として `AGENTS.md` を置いた。
- inbox → knowledge の流れを1回通した（2026-09-26、ZedへのVim環境移行のメモ → [[zed-vim]]）。統合時に実際の設定ファイルと照合し、メモと食い違う点が見つかった。

- Obsidian向けの作法を追加した。タグは `tags.md` の統制語彙による階層タグ、`aliases` で日本語名を付ける、知識一覧は `knowledge.base` で見る（[[ai-development-workflow]] D5）。
- `AGENTS.md` に、統合時に実物と照合する手順と、`Principles` / `Gotchas` の使い分けを追加した。

## Next Actions

- モバイルで壁打ちし、Obsidianモバイルアプリで inbox に保存して、Sync経由でPCに届くか試す（D4の検証）。
- `knowledge.base` をObsidianで開き、一覧が表示されるか確認する。
- Obsidian VaultをGit管理するか決める。
- Copilotを接続する。

## Goal

モバイルでのAI壁打ちをPC上のAI開発環境へ継続的に引き継ぐ。

## Current Architecture

```text
Mobile AI
  -> inbox (Markdown)
  -> knowledge / project context
  -> Obsidian / Git
  -> Zed
  -> ACP Agents
  -> Implementation / Validation
```

## Current Agents

- Codex via ACP
- Claude Agent via ACP
- 将来的にCopilot等も想定

## Source of Truth

AIサービスのチャット履歴ではなく、Markdownで管理するプロジェクト知識をSource of Truthとする。

## Current Decisions

- 会話ログは常設せず、根拠とハマりどころを知識へ統合する
- MarkdownをAI横断フォーマットとする
- Obsidianをナレッジ管理UIとして利用する
- ZedをPC側のAI開発UIとして利用する
- エージェントの入口は `AGENTS.md` に一本化する

## Open Questions

- Obsidian VaultをGit管理するか（Obsidian Syncとの併用要否）
- プロジェクトコンテキストをどこまで自動生成するか
