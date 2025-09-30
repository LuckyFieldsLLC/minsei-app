# Google 連携セットアップ手順

## 0. 事前
- 利用予定：Sign-In（Google Identity）、Drive（バックアップ）、Calendar（予定同期）
- 公開URL（Netlifyの本番URL）とローカル（http://localhost:5173 等）を控える

## 1. Google Cloud でプロジェクト作成
- APIs & Services > Credentials > 「+ Create Credentials」> **OAuth client ID**
- アプリ種別：**Web application**
- Authorized JavaScript origins：本番URL、開発URL（例：`https://minsei-katudou-shien.netlify.app` / `http://localhost:5173`）
- Authorized redirect URIs：Google Identity の実装に応じて設定（必要な場合のみ）

## 2. API を有効化
- 「Google Drive API」「Google Calendar API」を Enable

## 3. クライアントIDをアプリに設定
- アプリの **設定 > Google連携 > Client ID** に貼り付け

## 4. 権限
- 読み書きスコープは「バックアップ/復元」と「予定書き込み」に必要な最小限を使用
- 連携操作はユーザー明示操作（ボタン）を前提にする

## 5. 動作確認
- サインイン → Drive バックアップ作成/復元 → Calendar への予定登録
