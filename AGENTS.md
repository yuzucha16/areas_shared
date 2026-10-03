# AGENTS.md

このVault（`notes`）全体の規約。Claude / Codex / Copilot など、どのエージェントも同じルールで読み書きする。
各ディレクトリに固有のルールがある場合は、そのディレクトリの `AGENTS.md` / `CLAUDE.md` が優先される（例: `resources/exmem/AGENTS.md`）。

ObsidianはAI活用ナレッジの参照用で、新規作成はほぼしない。ノートの読み書きは、エージェントがファイルを直接行う。

## 共有とローカル

- Vaultのルート（`C:\vault\notes`）がそのままGitリポジトリ（GitHub: `yuzucha16/notes`）のルート。
- 共有（Git管理）するのは `resources/`、`.obsidian/`、ルートの `.gitignore` / `.gitattributes` / `AGENTS.md` / `CLAUDE.md` だけ。
- `projects/` `areas/` `archives/` はローカル専用。`.gitignore` のホワイトリスト（`/*` を除外して許可したものだけ追跡）で決まり、新しく作ったトップレベルのディレクトリも既定でローカル扱いになる。
- `resources/` の中は逆に、新しいものが既定で共有になる。ローカル専用のものは必ず `_local/` に置く。

## `_local/`

- どの階層の `_local/` も、中身はGitに載らない（`.gitkeep` だけ追跡する）。PCローカルのデータや、機密を置く場所。
- 検索や読み取りの対象。ただし内容を共有側のノートへ転記しない。
- `git add -f` で `_local/` や ignore 済みのファイルを追加しない。

## リンク

- 共有側（`resources/`）のノートから、ローカル側（`areas/` `projects/` `archives/` や `_local/`）へ `[[リンク]]` を張らない。他のPCでリンク切れになる。
- ノート間のリンクは wikilink（`[[名前]]`）。ファイル名はVault内で一意に保つ（最短パスで解決されるため）。

## `.obsidian/`

- Obsidianが起動中は、設定ファイル（`*.json`）を編集しない。Obsidianが上書きして、変更が消える。編集するときはObsidianを閉じる。
- `workspace.json` と `workspace-mobile.json` は端末ごとの状態なので、コミットしない（`.gitignore` 済み）。
- プラグインやテーマを追加・削除するときは、設定ファイルと `community-plugins.json` を合わせる。

## 書式とコミット

- 改行コードはLF（`.gitattributes` で統一）。
- コミットメッセージは `[領域] 変更内容` の形式（例: `[obsidian] material gruvbox`、`[exmem] ...`）。
- フォント・壁紙などのバイナリはGit LFS（`resources/fonts/` `resources/wallpapers/`）。`.gitattributes` を先に整えてから `git add` する。