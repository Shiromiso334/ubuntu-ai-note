# コンテンツ移行ログ

過去チャットから回収した記事や管理情報の移行履歴を記録するファイルです。
新たに移行・統合・修正があった場合は、日付付きで末尾に追記してください。

---

## 2026-03-10

### 既存記事を content-index.md に登録

- **対象**: ブログ記事 11本（B001〜B011）
- **状態登録**: B001〜B003 を「公開準備完了」、B004〜B011 を「下書き」として登録
- **元データ**: 複数チャットで作成された記事を `src/content/blog/` から統合
- **備考**: タイトル表記揺れやスラッグ不一致がある可能性があるため、今後の監査で順次確認予定

### 管理フロー整備

- `docs/editorial/` ディレクトリを新設
- `content-index.md`（正本一覧）・`status-board.md`（ダッシュボード）・`workflow.md`（運用ルール）を作成
- `content/drafts/` および `content/final/` ディレクトリ構造を整備

---

## 2026-03-11

### コンテンツID管理を導入

- `content-index.md` に「種別」カラムを追加
- ファイル命名規則を `Bxxx-スラッグ.md` 形式に統一（`content/drafts/` および `content/final/` 以下のみ）
- `src/content/blog/` 内の既存記事ファイル名は変更しない（Astroのルーティングに影響するため）
- `docs/editorial/migration-log.md`（このファイル）を新設
- `docs/editorial/topic-map.md` を新設
- `workflow.md` にID管理ルールを追記

## 2026-03-12

### Codex と Claude Code の連携運用に切り替え

- **対象**: プロジェクト全体
- **状態**: 会話中心運用 → task / log 中心運用
- **元データ**: 現行の `CLAUDE.md`、`docs/editorial/` 配下、運用方針メモ
- **備考**: `PROJECT_CONTEXT.md`、`docs/editorial/task-template.md`、`tasks/`、`logs/` を追加し、Codex が整理、Claude Code が実行、人間が承認する流れを明文化

### Ubuntu 側の task 自動実行基盤を追加

- **対象**: プロジェクト全体
- **状態**: 手動 task 実行のみ → 定期実行 / 手動実行 / 承認待ち対応あり
- **元データ**: `tasks/` 運用方針、Ubuntu 常駐実行の要件
- **備考**: `scripts/task-runner.sh`、`scripts/task-approval.sh`、`scripts/task-notify.sh`、`systemd/` 雛形、Telegram 通知対応を追加

### Claude 利用制限時のクールダウン再試行を追加

- **対象**: `scripts/task-runner.sh`
- **状態**: 制限到達時は一律 failed → `rate_limited` として一定時間後に再試行
- **元データ**: Claude Code の短時間制限に関する運用要件
- **備考**: `RATE_LIMIT_COOLDOWN_HOURS=5` を既定値として追加

### 人間確認後のブログ公開スクリプトを追加

- **対象**: ブログ公開フロー
- **状態**: 人間確認後も手動で複数操作 → `publish-blog.sh` で build / commit / push を一括実行
- **元データ**: 人間確認後はブログのみ自動反映したいという運用要件
- **備考**: X と note は対象外。ブログ記事のみローカルスクリプトで反映

### 人間確認待ちの Telegram 通知を追加

- **対象**: `scripts/task-runner.sh`
- **状態**: task 完了通知のみ → Human 担当・人間確認待ちコンテンツも通知
- **元データ**: B016 のようなレビュー待ち状態を Telegram で知りたいという要件
- **備考**: `tasks/notify/` に通知履歴を保存し、同じ内容の重複通知を避ける

### ブログ公開時の派生作業を自動化

- **対象**: `scripts/publish-blog.mjs`
- **状態**: ブログ反映のみ → トップページ導線更新と X 告知 task 起票も実施
- **元データ**: ブログ公開時にトップページ掲載調整と X 投稿文作成も進めたいという要件
- **備考**: X 投稿は作成・人間確認待ちまで自動、実投稿は人間が実施

### B017〜B020 の構成案と台帳登録を追加

- **対象**: B017, B018, B019, B020
- **状態**: 未登録 → 構成案作成・台帳登録済み
- **元データ**: Ubuntu入門シリーズの続きとトピックマップのギャップ
- **備考**: 初回セットアップ、日本語入力、ターミナル基本、メリット・デメリットの4本を先行登録

### Search Console 重複URL対策の手順を追加

- **対象**: Cloudflare 運用メモ
- **状態**: robots/sitemap のみ確認 → host 正規化ルールの設定値も文書化
- **元データ**: `http` / `https`、`www` ありなしの重複URL状況
- **備考**: `docs/editorial/cloudflare-redirect-rules.md` を追加

---

## ログの書き方テンプレート

```
## YYYY-MM-DD

### 作業内容タイトル

- **対象**: （コンテンツIDまたは種別）
- **状態**: （移行前 → 移行後）
- **元データ**: （チャット名・ファイルパスなど）
- **備考**: （気になる点・要確認事項）
```
