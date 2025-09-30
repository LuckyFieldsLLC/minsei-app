# 活動支援アプリ 基本設計 (v1.5.9)

> 本書は README の「仕様書」をもとに、実装視点の構成・画面・データ・連携を整理した基本設計です。運用での差分は本書と `CHANGELOG.md` を同期します。

## 1. 概要
- 目的：民生委員・児童委員の地域活動を支援する Web アプリ
- 特徴：オフラインファースト / レスポンシブ / PWA / AI・Google連携
- データ保管：**端末のブラウザ内に保存**（バックアップは JSON/Google Drive）

## 2. 非機能方針
- オフラインファースト：ブラウザ内ストレージ（IndexedDB/LocalStorage 実装に依存）
- PWA：ホーム画面追加、オフライン閲覧
- セキュリティ：個人データは端末内。外部送信はユーザー操作に基づく連携のみ（Drive/Calendar/AI）
- アクセシビリティ：ARIA / キーボード操作配慮
- 端末対応：スマホ～デスクトップまで

## 3. 構成（論理アーキテクチャ）
- フロントエンド：SPA（React + Vite）
- 永続化：ブラウザ内ストレージ（＋バックアップファイル/Google Drive）
- 外部連携：
  - Google Identity / Drive API / Calendar API
  - AI（Gemini / OpenAI）※APIキーはユーザー入力
- ホスティング：Netlify（静的ホスティング）

## 4. 画面とナビゲーション
- ダッシュボード：人数・ステータス別枚数、AIチェック通知、カードからフィルタ遷移
- 名簿一覧：検索・並び替え・フィルタ（地区/ステータス）
- 詳細画面：基本情報、活動履歴（追加/編集/削除/コピー共有）、AIメニュー
- 訪問予定：次回訪問の一覧と登録
- 活動月報：月次集計・コピー
- 設定：プロフィール/地区/表示/連携（AI, Google）
- AIチャット：自然言語検索、画像添付、要約/整形など

## 5. データモデル（概略）
> 厳密な実装は `types/` 等に準拠。ここでは仕様理解用の概略を示す。

```ts
type Status = '要検討'|'継続'|'入院中'|'廃止';

interface Person {
  id: string;             // uuid
  name: string;
  kana?: string;
  birthDate?: string;     // YYYY-MM-DD
  age?: number;           // 派生（表示時に計算可）
  gender?: '男'|'女'|'不明';
  address?: string;
  phone?: string;
  emergencyContact?: string;
  householdCategory?: string; // 世帯区分
  district?: string;      // 担当地区
  status: Status;
  nextVisitDate?: string; // YYYY-MM-DD
  nextVisitNote?: string;
  notes?: string[];       // ラベル/タグ等
  activities: Activity[];
  createdAt: string;      // ISO8601
  updatedAt: string;      // ISO8601
}

interface Activity {
  id: string;
  date: string;           // YYYY-MM-DD
  content: string;        // 活動メモ
  createdAt: string;
  updatedAt: string;
}
6. バックアップ/復元
CSV：名簿の入出力（住所/氏名/ふりがな/活動要約 等）

JSON：全データ（名簿/活動履歴/設定）を 1 ファイルで入出力

Google Drive：ワンクリックでバックアップ・復元

7. AI 機能（要 API キー）
自然言語検索・要約・文面整形、画像解析（予定表→カレンダー登録 等）

プロフィールを文脈に利用

起動時の自動チェック（更新提案）

料金：各社 API 従量課金。キーはユーザー入力で保持し、端末外へ保管しない

8. Google 連携
サインイン（Google Identity）

Drive バックアップ/復元

Calendar 予定同期（訪問予定/委員予定表）

初回セットアップ：Client ID 登録（手順は docs/google_integration.md）

9. 変更管理 / リリース
バージョン付与：v1.5.9 形式（CHANGELOG.md に記録）

README：概要/導入/主要リンク。詳細は docs/ に分割

Netlify：main ブランチ push で自動デプロイ

shell
コードをコピーする

---

4) もう一度 **Add file → Create new file**  
5) **`CHANGELOG.md`** を作成し、以下を貼り付け → **Commit changes**

### `CHANGELOG.md`（Keep a Changelog 風）
```markdown
# Changelog

すべての重要な変更はこのファイルで追跡します。

## [1.5.9] - 2025-10-01
### 変更
- ダッシュボードの表示設定を拡張（名簿カードの活動履歴を「最新/件数/非表示」切替）

## [1.5.8]
### 改善
- 内部的な機能整理

## [1.5.7]
### 追加
- 活動履歴の共有（詳細画面→履歴をコピー）

## [1.5.6]
### 追加
- 写真から委員予定表へカレンダー自動登録（AI）

## [1.5.5]
### 注意書き
- AI API 利用料金の注意喚起をヘルプ/設定に追記

## [1.5.4]
### 強化
- AIチャットの自然言語検索を強化（台帳データ文脈の理解）

## [1.5.3]
### UI
- Google連携ページを設定モーダルに集約

## [1.5.2]
### 追加/改善
- 「Google連携」新設、訪問予定からカレンダー登録

## [1.5.1]
### 追加
- Google Drive バックアップ/復元

## [1.5.0]
### 追加/強化
- バージョン履歴、ファイル/カメラ添付、プロフィール認識

## [1.4.2]
### 修正
- バージョン表示の内部修正

## [1.4.0]
### 追加
- AIアシスタント機能（要約/作成/提案/起動時チェック）

## [1.3.0]
### 追加/UI
- ダッシュボード/訪問予定/活動月報、SP下部ナビ導入

## [1.2.0]
### 追加
- データ管理（CSV, JSON バックアップ）

## [1.0.0]
### 初版
- 名簿 CRUD、活動履歴記録
