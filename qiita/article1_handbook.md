<!--
title: 【初心者向け】OpenClaw v2026.3.8 基本操作ハンドブック — AIエージェントと最初の一歩
tags: OpenClaw, Windows, AI, 環境構築, 初心者
-->

# 【初心者向け】OpenClaw v2026.3.8 基本操作ハンドブック

## はじめに

この記事では、次世代型AIエージェントツール **OpenClaw** のWindows環境へのインストールから初期設定までを、初心者向けにわかりやすく解説します。

実際にWindows 11環境で導入した実体験に基づいています。

> **📝 本記事は、筆者の実践経験に基づき、AI（Claude, Gemini, ChatGPT）を執筆補助ツールとして活用し作成しました。**

## OpenClawとは？

OpenClawは、PC上で自律的に動作し、複雑なタスクを共に解決してくれるAIエージェントツールです。ファイル操作、コード実行、Web検索、Discord連携など、多彩な機能をローカル環境で利用できます。

## 1. 事前準備：土台となるツールの導入

OpenClawを動かすには、以下の2つが必要です。

| ツール | 役割 | 確認コマンド | 目安 |
|---|---|---|---|
| **Node.js** | システム実行基盤（エンジン） | `node -v` | v22.0.0 以上 |
| **Git** | パッケージ管理（運び屋） | `git --version` | 2.x.x 以上 |

### Gitのインストール

```powershell
winget install --id Git.Git -e --source winget
```

> ⚠️ **インストール後は必ずPowerShellを再起動してください！** パスが反映されません。

### Node.jsのインストール

[Node.js公式サイト](https://nodejs.org/)からLTS版をダウンロード・インストールしてください。

## 2. OpenClawのインストール

### インストールコマンド

管理者権限のPowerShellで実行します：

```powershell
iwr -useb https://openclaw.ai/install.ps1 | iex
```

> ⚠️ `iex`（Invoke-Expression）はネット上のスクリプトを直接実行する強力なコマンドです。必ず公式（openclaw.ai）のような信頼できるソースであることを確認してから実行しましょう。

### 「用語として認識されません」と出たら？

PCを再起動しなくても、以下のコマンドでパスを強制反映できます：

```powershell
$env:Path = [System.Environment]::GetEnvironmentVariable("Path","Machine") + ";" + [System.Environment]::GetEnvironmentVariable("Path","User")
```

### 正常性確認

```powershell
openclaw --version
```

バージョンが表示されればインストール成功です！

## 3. オンボーディング：AIに「命」を吹き込む

```powershell
openclaw onboard --install-daemon
```

`--install-daemon` を付けることで、バックグラウンドサービスも同時にセットアップされます。

### モデル選択のガイド

| モデル | 特徴 | おすすめ用途 |
|---|---|---|
| `claude-opus-4-6` | 最高性能・高い論理推論能力 | 複雑なコーディング、プロジェクト管理 |
| `claude-3-7-sonnet-latest` | 速度と賢さのバランス | 日常的な対話、軽量な開発 |
| `claude-3-5-haiku-latest` | 格安かつ超高速 | 単純タスクの自動化 |

### APIキーの登録

```powershell
openclaw configure --section auth
```

## 4. Discord Bot連携

1. [Discord Developer Portal](https://discord.com/developers/applications) でApplicationを作成
2. Botトークンを発行
3. **Privileged Gateway Intents** を3つともONに設定：
   - ✅ Presence Intent
   - ✅ Server Members Intent
   - ✅ Message Content Intent
4. 起動後、Discord上でBotにメンションを送る
5. 発行されたペアリングコードを承認：

```powershell
openclaw pairing approve discord <コード>
```

## まとめ

OpenClawの導入は、依存関係（Node.js, Git）の準備さえ整えば、あとはスムーズに進みます。最初のセットアップを乗り越えれば、強力なAIパートナーとの共同作業が待っています！

次の記事では、WSL2を使ったより本格的な開発環境の構築を解説します。

## 関連リンク

- 📄 [GitHub: ドキュメント一式](https://github.com/akkiy6577/openclaw-windows-guide)
- 🌐 [OpenClaw 公式サイト](https://openclaw.ai)
- 📖 [OpenClaw ドキュメント](https://docs.openclaw.ai)

---

© 2026 Akihiko Hoshino | [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/deed.ja)
