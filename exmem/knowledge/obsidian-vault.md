---
type: knowledge
title: Obsidian Vault
status: active
tags:
  - tool/obsidian
  - knowledge-management
  - setup
  - backup
  - windows
aliases:
  - Obsidian Vault
  - Obsidianの設定
  - vaultのバックアップ
created: 2026-10-01
updated: 2026-10-02
sources:
  - Claude Code conversation "exmemの整理" (2026-09-26〜2026-10-01)
  - Claude conversation "vaultの置き場所とバックアップ方針" (2026-10-02)
  - "C:\\vault の構成とタスクスケジューラ（2026-10-02 に確認）"
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

## Vaultの置き場所とバックアップ

2026-10-02 のメモ（Claude conversation "vaultの置き場所とバックアップ方針"）から統合。

### Principles

- 作業場所とバックアップ先を分ける。OneDriveはバックアップ先として使い、作業場所にしない。
- バックアップは、まずrobocopyで始める。足りなければresticへ移行する。

### Decisions

#### vaultをOneDrive直下ではなくC直下に置く（2026-10-02）

- 根拠: 単一PC運用で複数端末の予定がなく、OneDrive同期のメリットが小さい。同期競合・ファイルロック・Files On-Demandによる遅延などを避けられる。
- 却下案: OneDrive直下のまま運用（「常にこのデバイス上に保持」やキャッシュ系の除外で回避する案）。`C:\Users\<名前>\vault`（OneDriveの外なら同期されないが、プロファイルと運命を共にし、パスがやや長い）。
- 実物（2026-10-02 確認）: vaultは `C:\vault\notes`（`C:\vault` 直下に `bin` / `certs` / `notes` / `repos` / `tools`）。メモの `C:\vault` はvault全体の置き場で、Obsidianのルートは `notes`。
- 注意: 「vault配下の `.git` は1つだけ」というメモの記述は、実物と違う。`C:\vault\notes` 直下に `.git` は無く、`.obsidian` と `areas_shared` がそれぞれ別のGitリポジトリへのジャンクション（上の表）。

#### バックアップはOneDriveへの定期コピー（robocopy + タスクスケジューラ）

- 根拠: C直下にすると自動バックアップが無くなるため。
- 初回は `/E`（追加・更新のみ、削除は反映しない）で運用する。`/MIR` は誤削除がバックアップにも波及するので見送る。
- 却下案: 最初から `restic`（世代管理付き）を導入する。
- コマンド案: `robocopy C:\vault "%OneDrive%\vault-backup" /E /XJ /R:2 /W:5 /XD .trash`
- 登録例: `schtasks /create /tn "vault-backup" /tr "C:\tools\vault-backup.bat" /sc daily /st 12:00`
- 実物（2026-10-02 確認）: `vault-backup` というタスクはタスクスケジューラに見当たらない。バックアップは未設定とみられる。

### Facts（メモ記載）

- OneDrive直下の問題: 同期競合コピー、ファイルロックによる保存失敗、Files On-Demandでgrep・AI読み込み時に遅延や一斉ダウンロード、小さなファイルの大量更新に弱い、パスが長く日本語・スペースを含みやすい、`.git` が壊れるリスク、同期停止に気づきにくい、組織アカウントのポリシー制約。`workspace.json` のような頻繁に書き換わる設定ファイルは競合の元で、シンボリックリンクの扱いも不安定。
- C直下の問題: 自動バックアップが無い、他端末・スマホから見られない。
- 「既知のフォルダーのバックアップ」が有効だと、Documents / Desktop / PicturesはOneDriveにリダイレクトされる。
- Windowsでシンボリックリンクを作るには開発者モードか管理者権限が必要。
- 仮説: ユーザー名が日本語やスペース入りなら `C:\vault` のほうがツール不具合を避けやすい。会社PCではC直下がIT部門のポリシーで制限される可能性がある（いずれも未確認）。

### Gotchas

- robocopyの `/XJ` はジャンクションをたどらない。実体が別のGitリポジトリ（`.obsidian` → dotfiles、`areas_shared`）なので、バックアップに含めたいか、`/XD` で外すかを決める。含めたいなら、リポジトリ側（GitHub）が別のバックアップになっている点も考える。
- PCが閉じていた日のバックアップを取りこぼさないよう、タスクスケジューラで「スケジュールされた時刻に開始できなかった場合、すぐにタスクを実行する」をオンにする。
- robocopyは「最新のコピー」しか持たず、過去の状態には戻れない。OneDriveのバージョン履歴とごみ箱で一部補える。
- 注意: このvaultはObsidian Syncも有効（上記）。OneDriveのバックアップ先とは独立している。

### Open Questions

- バックアップ対象にするジャンクション（`.obsidian`、`areas_shared`）と、除外の判断。
- 使っているPCが会社PCか（C直下の制約やバックアップポリシーに影響）。
- robocopyで足りるか、世代管理が必要になってresticへ移行するか。

### Next Actions

- `vault-backup.bat` を作り、ジャンクションの扱いを決めて `schtasks` に登録する（取りこぼし防止設定をオン）。
- 別フォルダへ復元し、Obsidianで開けるか確認する。

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
