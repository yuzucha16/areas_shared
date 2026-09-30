---
type: index
title: タグ一覧
status: active
tags:
  - knowledge-management
aliases:
  - Tags
created: 2026-09-26
updated: 2026-09-26
---

# タグ一覧

タグは「何についての知識か」を表す。新しいタグは、ここに追記してから使う。

## ルール

- 英小文字の kebab-case。日本語・スペースは使わない。
- 1ノートあたり 3〜6 個を目安にする。
- ソフトウェアとAIは階層タグにする。Obsidianで `tag:#tool` と検索すると `tool/*` がすべて引っかかる。
- `type` や `status` の値はタグにしない。
- 「AI」「メモ」のように、ほぼ全ノートに付くタグは作らない。絞り込みに役立たないため。

## 語彙

### `tool/` — ソフトウェア

| タグ | 意味 |
|---|---|
| `tool/zed` | Zedエディタ |
| `tool/vim` | Vim |
| `tool/neovim` | Neovim |
| `tool/obsidian` | Obsidian |

### `ai/` — AIサービス・エージェント

| タグ | 意味 |
|---|---|
| `ai/chatgpt` | ChatGPT（モバイル・Webのチャット） |
| `ai/codex` | Codex |
| `ai/claude` | Claude / Claude Agent |
| `ai/copilot` | GitHub Copilot |

### トピック

| タグ | 意味 |
|---|---|
| `workflow` | 作業の流れ・運用 |
| `knowledge-management` | 知識の整理・保存方法 |
| `context-engineering` | AIへ渡すコンテキストの設計 |
| `acp` | Agent Client Protocol |
| `keymap` | キーバインド |
| `setup` | インストール・初期設定の手順 |
| `mobile` | モバイル端末での利用 |
