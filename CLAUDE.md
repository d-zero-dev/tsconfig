# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 概要

D-ZERO 株式会社の共有 TypeScript 設定パッケージ (`@d-zero/tsconfig`)。`@tsconfig/recommended`、`@tsconfig/strictest`、`@tsconfig/node-lts` をベースに、Node.js / フロントエンド共通の `tsconfig.json` を提供する。npm パッケージとして公開される（シングルパッケージ）。

## プロジェクト構成

作業前に以下のファイルを確認し、プロジェクトの状態を把握すること:

- `package.json` — `dependencies`（@tsconfig/\* のベース構成）、scripts、Volta（Node 24 / Yarn 4）
- `tsconfig.json` — 公開対象の TypeScript 設定（`files` に列挙）
- `README.md` — パッケージ概要

## コマンド

- `yarn lint` — `prettier --write *.{md,json}`（フォーマット）
- `yarn release:major` / `release:minor` / `release:patch` / `release:alpha` / `release:beta` / `release:rc` — `npm version` のみ実行（tag push で publish.yml が npm publish を行う）
- `yarn update` — `yarn upgrade-interactive`

### コマンド制約

- **yarn のみ使用**: npm / pnpm / bun / deno によるコマンド実行は禁止（`yarn release:*` の中で `npm version` を呼ぶのは規定の挙動）
- **コマンドの連続実行禁止**: `&&`、`;`、改行によるコマンド連結をしない。1回の Bash 呼び出しで1コマンドのみ実行する。連結されたコマンドは settings.json の permissions allow/deny でパターンマッチできず、毎回ユーザーの手動承認が必要になり効率が大幅に低下する

## 配布物

`package.json` の `files` フィールドで `tsconfig.json` のみを公開している。新規ファイルを公開対象に追加する場合は `files` を更新すること。

## セキュリティ

### 機密情報の取り扱い

- `.env`、`.env.*` 等の機密ファイルを読み取り・編集・コミットしない（機密ファイルの判断は `.gitignore` を参考にすること）
- コミット前に `git diff --staged` で機密情報（API キー、トークン、パスワード、企業名、顧客情報）が含まれていないか確認する
- 環境変数やシークレットをコード内にハードコードしない

### サプライチェーン保護

- **yarn dlx は完全禁止**: ローカルパッケージを使わずリモートから直接実行するため、サプライチェーン攻撃に脆弱
- **npx は原則使わない**: package.json の scripts で定義されたコマンドを `yarn <script>` で実行すること
- 新しい依存パッケージの追加は慎重に。既存の依存で解決できないか先に確認する
- `yarn add` する前にパッケージの信頼性（ダウンロード数、メンテナンス状況、既知の脆弱性）を確認する
- `yarn add` する場合はバージョンを固定する（例: `yarn add foo@1.2.3`）
- lockfile（yarn.lock）の手動編集は禁止
