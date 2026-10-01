---
type: knowledge
title: Obsidian Vault
status: active
tags:
  - tool/obsidian
  - knowledge-management
  - setup
aliases:
  - Obsidian Vault
  - Obsidianの設定
created: 2026-10-01
updated: 2026-10-01
sources:
  - Claude Code conversation "exmemの整理" (2026-09-26〜2026-10-01)
  - "C:\\vault\\notes\\.obsidian の設定ファイル（2026-10-01 に確認）"
---

# Obsidian Vault

## Purpose

このナレッジベース（exmem）を閲覧・管理しているObsidian Vaultの環境と、ナレッジベースから使っている機能をまとめる。

## Vault

2026-10-01 時点。

- Vaultのルート: `C:\vault\notes`
- 直下はPARA形式: `projects/` / `areas/` / `resources/` / `archives/`
- このナレッジベースの場所: `areas_shared/exmem`

一部のフォルダはGitリポジトリへのジャンクションになっている。

| Vault内のパス | 実体 | Gitリモート |
|---|---|---|
| `.obsidian` | `C:\vault\repos\github.com\yuzucha16\dotfiles\obsidian\.obsidian` | dotfiles |
| `areas_shared` | `C:\vault\repos\github.com\yuzucha16\areas_shared` | `https://github.com/yuzucha16/areas_shared` |

したがって、このナレッジベースは `areas_shared` リポジトリでGit管理されている。変更は `git diff` で確認できる。

## 設定

2026-10-01 時点で `.obsidian` の設定ファイルから確認した内容（2026-09-26 時点と同じ）。

### コアプラグイン

- 有効: Sync、Bases、Templates、Backlinks、Graph、Tag pane、Daily notes、Canvas など
- 無効: Properties view

### コミュニティプラグイン

- `calendar`
- `obsidian-icon-folder`
- `colored-tags`（タグを色分けする。階層タグの親ごとに色が変わる）

### その他

- 新規ノートの保存先 `newFileFolderPath`: `0_inbox`（このフォルダはVaultに存在しない）
- 添付ファイルの保存先 `attachmentFolderPath`: `0_inbox`

## ナレッジベースから使っている機能

| 機能 | 使い方 |
|---|---|
| Obsidian Sync | モバイルアプリで `inbox/` に保存したノートをPCへ届ける（[[ai-development-workflow]] D4、未検証） |
| Bases | `knowledge.base` で知識・プロジェクト・inboxの一覧表を表示する（表示は未確認） |
| 階層タグ + `colored-tags` | `tags.md` の統制語彙（[[tags]]） |
| `aliases` | 英語ファイル名のノートを日本語でリンク補完・検索する |
| Backlinks / Graph | `## Related` の `[[リンク]]` でノート間のつながりを見る |

## Gotchas

### Vaultを移したあと、古い場所を編集していた

- 状況: 2026-10-01 にナレッジベースを `C:\Users\ck\vault\notes` 配下から `C:\vault\notes\areas_shared\exmem` へ移したが、AIエージェントは古い場所を作業ディレクトリとして開いたまま編集を続けた。
- 解決: 変更を exmem へ移し、古い場所は削除した。エージェントは `C:\vault\notes\areas_shared\exmem` を作業ディレクトリとして起動する。

## Proposals

Vault全体に影響し、Syncで他の端末にも伝わるため、まだ適用していない。

- 新規ノートの保存先を `areas_shared/exmem/inbox` にする。モバイルで新規ノートを作るだけで inbox に入る。
- `created` / `updated` のプロパティ型を「日付」にする。Basesでの並べ替えや日付フィルタが正しく動く。
- Templatesで知識ノート用のテンプレートを作る。PCで直接書くときにfrontmatterを毎回手で打たずに済む。

## Related

- [[ai-development-workflow]]
- [[ai-development-workflow/context]]
- [[tags]]
