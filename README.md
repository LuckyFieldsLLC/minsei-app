# 活動支援アプリ（Community Contact Ledger）

**バージョン:** v1.5.9  
**開発者:** LuckyFields.LLC  
**最終更新日:** 2025-10-01

---

## 📘 概要

民生委員・児童委員の地域活動を支援するWebアプリケーションです。  
紙やスプレッドシートによる管理をデジタル化し、スマートフォンやPCから  
名簿・活動履歴・予定を一元管理できます。

**主な特徴：**
- オフライン対応（ローカルストレージ保存）
- PWA対応（ホーム画面に追加可）
- AI連携による支援（Gemini / OpenAI）
- Googleサービスとの連携（Drive / Calendar）

---

## 📂 ドキュメント一覧

| ドキュメント名 | 内容 | リンク |
|----------------|------|--------|
| 基本設計書 | アプリ全体の設計・仕様を記載 | [docs/basic_design.md](docs/basic_design.md) |
| AI機能仕様書 | Gemini / OpenAI連携の詳細仕様 | [docs/ai_features.md](docs/ai_features.md) |
| Google連携手順書 | Googleアカウント連携・バックアップ・カレンダー同期の手順 | [docs/google_integration.md](docs/google_integration.md) |
| 更新履歴 | 各バージョンの変更点 | [CHANGELOG.md](CHANGELOG.md) |

---

## 🚀 セットアップ手順

### 1. リポジトリをクローン
```bash
git clone https://github.com/【あなたのユーザー名】/minsei-app.git
cd minsei-app
2. 依存関係をインストール
bash
コードをコピーする
npm install
3. 開発サーバーを起動
bash
コードをコピーする
npm run dev
→ ブラウザで http://localhost:5173 にアクセス

⚙️ 環境変数設定
.env.local に以下を記載してください：

bash
コードをコピーする
VITE_GOOGLE_CLIENT_ID=your_google_client_id
VITE_OPENAI_API_KEY=your_openai_api_key
🧠 主な機能
名簿管理（登録・検索・フィルタ・ソート）

活動履歴記録（音声入力・コピー共有）

訪問予定管理（Googleカレンダー同期可）

AIチャットによる検索・要約・提案

Googleドライブ連携バックアップ

詳細は docs/basic_design.md を参照。

🧩 技術スタック
フロントエンド: Vite + React + TypeScript

スタイル: Tailwind CSS

データ保存: localStorage / Google Drive

AI連携: Gemini API / OpenAI API

PWA: Service Worker + Manifest

🗓 バージョン履歴
最新バージョン：v1.5.9
詳しくは CHANGELOG.md を参照。

📄 ライセンス
© 2025 LuckyFields.LLC. All Rights Reserved.

