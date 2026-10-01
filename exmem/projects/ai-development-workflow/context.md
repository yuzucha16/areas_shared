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
updated: 2026-10-01
---

# AI開発ワークフロー Project Context

## Current State

- ZedにCodexとClaude AgentをACPで接続済み（[[zed-acp]]）。
- ナレッジ構成を `inbox/` → `knowledge/` → `projects/` の形に整理した。会話ログは常設しない（[[ai-development-workflow]] D2）。
- 各エージェントの入口として `AGENTS.md` を置いた（D6）。
- Obsidian向けの作法を追加した。タグは `tags.md` の統制語彙による階層タグ、`aliases` で日本語名を付ける、知識一覧は `knowledge.base` で見る（D5、D9）。
- inbox → knowledge の流れを3回通した。毎回、実物との照合でメモとの食い違いが見つかった。
  - 2026-09-26: ZedへのVim環境移行のメモ → [[zed-vim]]
  - 2026-10-01: このナレッジベース整備の会話メモ → [[ai-development-workflow]]（Principles、D6〜D9、Gotchas）と [[obsidian-vault]]
  - 2026-10-01: Zedのdotfiles管理とClaudeチャット履歴のメモ → [[zed-dotfiles]] と [[claude-code-storage]]
- 2026-10-01 に作業拠点を `C:\Users\ck\vault\notes` から `C:\vault\notes` へ移した。
  - ナレッジベースは `areas_shared/exmem`。`areas_shared` はGitリポジトリ（yuzucha16/areas_shared）で、Git管理になった（[[obsidian-vault]]）。
  - Vaultのルートに、エージェント向けの入口 `AGENTS.md` / `CLAUDE.md` を置いた。どこから起動してもexmemの場所がわかる。
  - Claude Codeの履歴とメモリを `C--vault-notes` へコピーした（[[claude-code-storage]]）。
  - 古い場所（`C:\Users\ck\vault`）と、Downloadsにあった整理前のコピーは削除した。
- inbox は空。

## Next Actions

- Claude Codeを `C:\vault\notes` で起動し、コピーした履歴とメモリが引き継がれているか確認する。
- `knowledge.base` をObsidianで開き、一覧が表示されるか確認する。
- モバイルで壁打ちし、Obsidianモバイルアプリで inbox に保存して、Sync経由でPCに届くか試す（D4の検証）。
- Obsidianの設定変更（新規ノートの保存先・日付型・テンプレート）を判断する（[[obsidian-vault]] Proposals）。
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

- GitとObsidian Syncをどう使い分けるか。exmemは `areas_shared` リポジトリでGit管理され、VaultではObsidian Syncも有効になっている。
- Downloads（`C:\Users\ck\Downloads\ai-workflow-notes`）に残っている整理前のコピーを削除するか。
- プロジェクトコンテキストをどこまで自動生成するか
