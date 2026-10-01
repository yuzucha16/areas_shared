---
type: index
title: AI開発ワークフロー
status: active
tags:
  - workflow
  - knowledge-management
  - tool/obsidian
aliases:
  - exmem
  - ai_workflow_notes
created: 2026-09-26
updated: 2026-10-01
---

# AI開発ワークフロー

## 目的

モバイルで行ったAIとの壁打ちを、PCのZed上でClaude / Codex / Copilotなど複数のAIエージェントに引き継ぎ、実装・検証までつなげる。

基本方針は、**会話ログを溜めずに、知識として育てる**こと。
会話の根拠（なぜそう決めたか）とハマりどころは、知識ファイルの中に残す。

- `inbox/`: 未整理の会話メモの一時置き場。知識へ統合したら削除する
- `knowledge/`: AIをまたいで再利用する知識。1ファイル1トピック
- `projects/`: 個別プロジェクトの現在状態と次にやること

## ディレクトリ構造

場所は `C:\vault\notes\areas_shared\exmem`（Obsidian Vault `C:\vault\notes` の中）。`areas_shared` リポジトリでGit管理している。
旧名は `ai_workflow_notes`。AIエージェントはこのディレクトリを作業ディレクトリとして起動する。

```text
exmem/
├── README.md
├── AGENTS.md          # 全エージェント共通の入口・書き方ルール
├── CLAUDE.md          # @AGENTS.md を読み込むだけ
├── tags.md            # タグの語彙とルール
├── knowledge.base     # Obsidian Bases: 知識・プロジェクトの一覧表
├── inbox/
│   └── README.md      # モバイル用の引き継ぎプロンプト
├── knowledge/
│   ├── ai-development-workflow.md
│   ├── claude-code-storage.md
│   ├── obsidian-vault.md
│   ├── zed-acp.md
│   ├── zed-dotfiles.md
│   └── zed-vim.md
└── projects/
    ├── ai-development-workflow/
    │   └── context.md
    └── zed-vim-migration/
        └── context.md
```

Zed ACPは独立したプロジェクトではなく、AI開発ワークフローを構成する要素の一つとして `knowledge/zed-acp.md` で扱う。

## AI横断性

これらのMarkdownは、特定AIの固有フォーマットを前提にしない。

- Claude
- Codex / GPT
- GitHub Copilot
- その他のMarkdownを読めるAI

が同じファイルをコンテキストとして利用できることを前提とする。

エージェント向けのルールは `AGENTS.md` に一本化する。AI固有の設定が必要な場合は、知識本文ではなく各ツール側の設定として分離する。

## 運用ルール

1. 壁打ちの最後に `inbox/README.md` のプロンプトで要点をまとめさせ、Obsidianモバイルアプリで `inbox/` に保存する。
2. inbox のメモから決定・根拠・ハマりどころ・未決事項を `knowledge/` に統合し、メモは削除する。
3. プロジェクト固有の現在状態は `projects/<project>/context.md` に集約する。
4. 作業の終わりに `context.md` の `Current State` と `Next Actions` を更新する。
5. AIを変更しても読めるよう、Markdown + YAML frontmatter + 通常の見出しを基本とする。

詳しい書き方は `AGENTS.md` を参照。
