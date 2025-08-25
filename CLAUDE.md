# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Development Commands

### Frontend Development
- `npm run dev` - フロントエンド開発サーバーを起動 (Vite)
- `npm run build` - プロダクション用TypeScriptコンパイル＆ビルド
- `npm run preview` - ビルド済みファイルのプレビュー

### Tauri Development
- `npm run tauri dev` - Tauriアプリケーションの開発モードで起動（フロントエンド＋Rustバックエンド）
- `npm run tauri build` - Tauriアプリケーションのプロダクションビルド

## Architecture Overview

このプロジェクトはTauri v2を使用したハイブリッドデスクトップアプリケーションです。

### Frontend (React + TypeScript + Vite)
- `src/` - Reactアプリケーションのソースコード
- `src/main.tsx` - アプリケーションのエントリーポイント
- `src/App.tsx` - メインアプリケーションコンポーネント
- `index.html` - HTMLテンプレート
- `vite.config.ts` - Vite設定（ポート1420で固定、HMRはポート1421）

### Backend (Rust)
- `src-tauri/src/lib.rs` - Tauriコマンド定義とアプリケーション設定
- `src-tauri/src/main.rs` - Rustアプリケーションのエントリーポイント
- `src-tauri/Cargo.toml` - Rust依存関係とビルド設定
- `src-tauri/tauri.conf.json` - Tauriアプリケーション設定

### Frontend-Backend Communication
- `@tauri-apps/api/core`の`invoke`を使用してRustコマンドを呼び出し
- 現在実装されているコマンド:
  - `greet(name: string)` - 文字列を返すサンプルコマンド（コメントアウト中）
  - `my_custom_command()` - コンソールにログ出力するカスタムコマンド

### Build Configuration
- フロントエンドは`dist/`にビルドされ、Tauriが`frontendDist`として参照
- 開発時は`beforeDevCommand`でフロントエンド開発サーバーを自動起動
- ビルド時は`beforeBuildCommand`でフロントエンドを事前ビルド