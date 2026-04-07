# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

D-ZERO社の共有TypeScript設定パッケージ (`@d-zero/tsconfig`)。
`@tsconfig/recommended`, `@tsconfig/strictest`, `@tsconfig/node-lts` をベースに、Node.js・フロントエンド共通のtsconfig設定を提供する。npmパッケージとして公開される。

## Commands

- **Lint/Format**: `yarn lint` (prettierによるmd/jsonファイルのフォーマット)
- **依存更新**: `yarn update` (upgrade-interactive)
- **リリース**: `yarn release:major` / `yarn release:minor` / `yarn release:patch` (npm version のみ。tag push で GitHub Actions が npm publish)

## Tech Stack

- **Package Manager**: Yarn 4 (nodeLinker: node-modules)
- **Node**: Volta管理 (v24)
- **配布物**: `tsconfig.json` のみ (`files` フィールドで指定)
