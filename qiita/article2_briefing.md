<!--
title: 【実践編】OpenClaw + WSL2 で作るWindows開発環境 — Python/C++をLinuxネイティブで動かす
tags: OpenClaw, WSL2, Python, C++, VSCode
-->

# 【実践編】OpenClaw + WSL2 で作るWindows開発環境

## はじめに

[前回の記事](※リンク)でOpenClawの基本セットアップを完了しました。本記事では、Windows上でWSL2を活用し、Python/C++のLinuxネイティブな開発環境を構築する手順を実践的にまとめます。

さらに、OpenClawの構成設定の詳細やトラブルシューティングも解説します。

> **📝 本記事は、筆者の実践経験に基づき、AI（Claude, Gemini, ChatGPT）を執筆補助ツールとして活用し作成しました。**

## 1. OpenClawのトラブルシューティング

### 1.1 依存関係の解消

初期セットアップでよく遭遇する問題と解決策：

| 症状 | 原因 | 解決策 |
|---|---|---|
| `ENOENT` エラー | Node.js未導入 | Node.js LTS版をインストール |
| `npm` が認識されない | PATH未反映 | シェル再起動 or 環境変数リロード |
| インストーラーが失敗 | Git未導入 | `winget install --id Git.Git` |

### 1.2 診断ツール

```powershell
openclaw doctor
```

設定ファイルの不備を自動検出し、`--fix` オプションで修復が可能です。

## 2. 構成設定（openclaw.json）の詳細

### 2.1 v2026.3.8 での変更点

**認証プロファイルの構造変更：**
```json
{
  "auth": {
    "profiles": {
      "anthropic": {
        "provider": "anthropic",
        "mode": "api_key"
      }
    }
  }
}
```

`auth` 直下ではなく、`auth.profiles.anthropic` のように階層化されています。

**ゲートウェイ設定の変更：**
```json
{
  "gateway": {
    "bind": "loopback",
    "port": 18789
  }
}
```

従来のIP指定（`127.0.0.1`）から、`loopback` 等のモード指定に移行しています。

### 2.2 ポート衝突の解決

ゲートウェイが使用するポート（18789）が既に占有されている場合：

```powershell
schtasks /End /TN "OpenClaw Gateway"
```

## 3. WSL2による開発環境の構築

### 3.1 WSL2の有効化

管理者権限のPowerShellで実行：

```powershell
# WSLとVirtualMachinePlatformを有効化
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

**PCを再起動後：**

```powershell
wsl --install -d Ubuntu
```

### 3.2 開発スタックのセットアップ

Ubuntu上で以下を実行：

```bash
# システム更新
sudo apt update && sudo apt upgrade -y

# Python環境
sudo apt install python3 python3-pip python3-venv -y

# C++開発ツール（gcc, g++, make を含む）
sudo apt install build-essential -y
```

### 3.3 バージョン確認

```bash
python3 --version   # Python 3.x.x
g++ --version        # g++ 13.x.x
gcc --version        # gcc 13.x.x
```

## 4. VS Code Remote連携

### 4.1 必要な拡張機能

VS Codeに以下をインストール：

- **WSL** — WSL2内のファイルを直接編集
- **Python** — Python開発サポート
- **C/C++** — C++開発サポート

### 4.2 WSL側のプロジェクトをVS Codeで開く

```powershell
# PowerShellから直接WSL側のフォルダを開ける
code --remote wsl+Ubuntu /home/akkiy/projects/cpp
```

これにより、Windows上のVS Codeから、WSL2内のLinuxファイルシステムをネイティブに操作できます。

## 5. 外部サービスの連携

### Web検索
Google Search（Gemini API）等を連携させることで、エージェントがオンライン情報を取得可能になります。

### Google Chat
サービスアカウントのJSONファイルとWebhook URLの設定により、Google Chat上での運用もサポートされています。

## まとめ

WSL2とVS Code Remoteの組み合わせにより、Windows上でLinuxネイティブな開発環境が手に入ります。OpenClawと合わせることで、AI支援付きのクロスプラットフォーム開発が実現できます。

次の記事では、運用フェーズでの標準手順（SOP）を解説します。

## 関連リンク

- 📄 [GitHub: ドキュメント一式](https://github.com/akkiy6577/openclaw-windows-guide)
- 🌐 [OpenClaw 公式サイト](https://openclaw.ai)
- 📖 [OpenClaw ドキュメント](https://docs.openclaw.ai)

---

© 2026 Akihiko Hoshino | [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/deed.ja)
