# CLAUDE.md — Ubuntu×AI実践ノート 運用ルール

## このブログの目的

- Ubuntu、Claude Code、AI作業環境の構築と実践を記録するブログ
- 想定読者：Ubuntuを導入したばかりの初心者、AIで作業効率化や副業環境を整えたい人

## 記事作成の基本方針

- 日本語で書く
- 英語のダミーテキストは使わない
- 誇張表現は避ける
- 初心者向けに分かりやすく書く
- 実体験ベースで違和感のない文章を優先する
- 文体は「です・ます調」で統一する
- ブログ全体の文体・人格の一貫性を優先すること
- 勝手に文体を変えないこと

## 執筆時の参照ファイル

記事を執筆・編集する際は、必ず以下のファイルを参照すること。

- `docs/author-persona.md` — 執筆者の人格・価値観・読者への向き合い方
- `docs/writing-style.md` — 文体ルール・語尾バリエーション・構成の基本
- `docs/article-template.md` — 記事テンプレート（フロントマター〜締めまで）

記事生成後は `docs/ai-writing-fixes.md` を使って品質チェックとリライトを行うこと。

## 固定ページ運用

- `about` / `contact` / `privacy` / `disclosure` を維持する
- 既存の固定ページ導線（ヘッダー・フッターのリンク）を壊さない

## 記事追加時のルール

- フロントマターに `title` / `description` / `pubDate` / `tags` を設定する
- 関連する既存記事への内部リンク（「あわせて読みたい」セクション）を検討する
- 必要ならトップページ（`src/pages/index.astro`）の導線も追加する

## デザイン変更の方針

- 最小限を優先する
- 大きなレイアウト変更は勝手に行わない

## コンテンツ管理フロー

制作管理は `docs/editorial/` 以下のファイルで行う。

- `docs/editorial/content-index.md` — 全コンテンツの正本一覧（状態管理）
- `docs/editorial/status-board.md` — 作業優先度ダッシュボード
- `docs/editorial/workflow.md` — チャット役割分担・運用ルール定義
- `docs/editorial/migration-log.md` — 移行・統合・修正の履歴
- `docs/editorial/topic-map.md` — SEO構造・テーマ一覧

下書きは `content/drafts/`、最終稿は `content/final/` に保存すること。
新規コンテンツ作成・状態変更のたびに `content-index.md` を更新すること。

## 作業時の注意

- 既存記事の主内容を不要に書き換えない
- 他ページに影響する変更は最後に報告する
- 変更・作成したファイル名を最後に報告する
