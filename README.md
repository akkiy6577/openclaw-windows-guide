# OpenClaw Windows 環境導入・運用ガイド

OpenClaw v2026.3.8 の Windows 環境における導入から運用までを体系的にまとめたドキュメント集です。

## 📚 ドキュメント一覧

| ファイル | 内容 | 対象読者 |
|---|---|---|
| [OpenClaw_Handbook.pdf](./OpenClaw_Handbook.pdf) | 基本操作ハンドブック — 初めてのセットアップ | 初心者向け |
| [OpenClaw_Briefing.pdf](./OpenClaw_Briefing.pdf) | 総合ブリーフィング — 環境構築の詳細分析 | 中級者向け |
| [OpenClaw_Windows_SOP.pdf](./OpenClaw_Windows_SOP.pdf) | 標準運用マニュアル（SOP） | 管理者・運用担当向け |

## 🔧 対象環境

- **OS:** Windows 10 / 11
- **サブシステム:** WSL2 (Ubuntu)
- **対象バージョン:** OpenClaw v2026.3.8
- **AIモデル:** Anthropic Claude (Opus 4.6 / Sonnet / Haiku)

## 📖 内容の概要

### 基本操作ハンドブック
- Node.js / Git の導入
- OpenClaw のインストールとセキュリティ設定
- オンボーディング（AIプロバイダー・モデル選択）
- Discord Bot 連携

### 総合ブリーフィング
- トラブルシューティングと依存関係の解消
- 構成設定（openclaw.json）の詳細
- WSL2 による Python / C++ 開発環境の構築
- VS Code Remote 連携

### 標準運用マニュアル（SOP）
- システム要件と環境構築の事前準備
- PowerShell 実行ポリシーの管理
- OneDrive パス干渉の回避策
- デプロイメント手順と正常性確認

## 🤖 AI活用について

本ドキュメントは、筆者の実践経験に基づき、AI（Claude, Gemini, ChatGPT）を執筆補助ツールとして活用し作成しました。

## 📜 ライセンス

© 2026 Akihiko Hoshino. All rights reserved.

本ドキュメントは [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/deed.ja) ライセンスの下で公開しています。

## 🔗 関連リンク

- [OpenClaw 公式サイト](https://openclaw.ai)
- [OpenClaw ドキュメント](https://docs.openclaw.ai)
- [OpenClaw GitHub](https://github.com/openclaw/openclaw)
- [OpenClaw コミュニティ (Discord)](https://discord.com/invite/clawd)
