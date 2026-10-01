---
type: knowledge
title: Claude Codeのチャット履歴とメモリの保存場所
status: active
tags:
  - ai/claude
  - tool/zed
  - dotfiles
  - setup
aliases:
  - Claude Codeの履歴の保存場所
  - Claudeチャット履歴の移行
created: 2026-10-01
updated: 2026-10-01
sources:
  - Claude (Claude Code via Zed ACP) conversation "Claudeチャット履歴の保存場所" (2026-10-01)
  - "C:\\Users\\ck\\.claude\\projects（2026-10-01 に確認）"
---

# Claude Codeのチャット履歴とメモリの保存場所

## Purpose

Claude Code（ZedのACP経由を含む）のチャット履歴とメモリがどこに保存され、プロジェクトを移動したときにどう引き継ぐかをまとめる。

## 保存場所

2026-10-01 時点で確認済み。

| 中身 | 場所 |
|---|---|
| チャット履歴 | `%USERPROFILE%\.claude\projects\<プロジェクト名>\<session-id>.jsonl` |
| メモリ | `%USERPROFILE%\.claude\projects\<プロジェクト名>\memory\` |
| プロジェクトごとの許可設定 | `<プロジェクト>\.claude\settings.local.json` |

- `<プロジェクト名>` は、プロジェクトの絶対パスの `:` `\` `.` を `-` に置き換えたもの。
  - `C:\vault\notes` → `C--vault-notes`
  - `C:\Users\ck\vault\github.com\yuzucha16\notes` → `C--Users-ck-vault-github-com-yuzucha16-notes`
- 1チャット = 1ファイル。隠しファイルではない。
- プロジェクト直下の `.claude\` にあるのは `settings.local.json` だけで、履歴は入っていない。
- ZedのACP経由のチャットも、Zedの `threads.db` ではなくここに保存される（[[zed-dotfiles]]）。
- Claude Desktop の Projects はクラウド（アカウント側）に保存され、`~/.claude` のローカル履歴とは独立している。

## プロジェクトを移動したとき

履歴とメモリはプロジェクトの絶対パスごとに分かれるため、プロジェクトを移動すると前のチャットやメモリが見えなくなる。

引き継ぐには、`projects\<旧プロジェクト名>\` の `.jsonl` と `memory\` を `projects\<新プロジェクト名>\` にコピーする。

2026-10-01 に、`C:\Users\ck\vault\notes` から `C:\vault\notes` への移動でこの方法を使った（`C--Users-ck-vault-notes` → `C--vault-notes`）。コピーした履歴が新しい場所で表示されるかは未確認（仮説）。

## Decisions

### チャット履歴（`.jsonl`）はdotfilesに含めない（2026-10-01）

- 根拠: サイズが大きくなりやすく、会話の中身がそのまま入っている。
- 却下案: `~/.claude` 全体をdotfilesに入れる。

## Gotchas

### `.claude` をコピーしたのに、移動先でチャットが見えない

- 原因: コピーしたのはプロジェクト直下の `.claude`（設定のみ）だった。履歴はユーザーフォルダ直下の `%USERPROFILE%\.claude\projects\` にある。名前が同じ別のフォルダ。
- 解決: ユーザーフォルダ側の `projects\<旧プロジェクト名>\*.jsonl` を `projects\<新プロジェクト名>\` にコピーする。

### `.jsonl` が見つからない

- 原因: プロジェクト内の `.claude` を見ていた。隠し属性ではない。
- 解決: エクスプローラーのアドレスバーに `%USERPROFILE%\.claude\projects` を入力して開く。

### Claude Desktop の Projects に履歴が出ない

- 原因: 不具合ではない。Desktop の Projects はクラウド、Claude Code の履歴はローカルで、保存先が別。

## Open Questions

- `~/.claude` の手書き設定（`CLAUDE.md`、`settings.json`、`projects\<プロジェクト名>\memory\`）をdotfilesで管理するか。
- Claude Desktop の Code 機能から、ローカルの履歴が見えるか。

## Next Actions

- Claude Codeを `C:\vault\notes` で起動し、コピーした履歴が表示されるか確認する。

## Related

- [[zed-dotfiles]]
- [[zed-acp]]
- [[obsidian-vault]]
