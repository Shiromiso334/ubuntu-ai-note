# コンテンツ制作ワークフロー

このファイルは、ブログ・X・noteの制作・管理フローを定義します。
チャットを使い分けて役割を分担し、ファイルを正本として運用します。

---

## チャットの役割分担

### 記事制作チャット

- **目的**: 新しい記事・投稿の文章を作る
- **入力**: テーマ・構成メモ・キーワードなど
- **出力**: `content/drafts/` 以下に下書きファイルを保存
- **参照必須**:
  - `docs/author-persona.md`（執筆者の人格・語り口）
  - `docs/writing-style.md`（文体ルール・語尾バリエーション）
  - `docs/article-template.md`（記事テンプレート）
- **注意**: 文体は「です・ます調」で統一。誇張表現・英語ダミーテキスト禁止

---

### 監査チャット

- **目的**: 下書きをレビューし、品質を確認する
- **入力**: `content/drafts/` 内の下書きファイル
- **出力**: 修正指摘をファイル末尾または別ファイルにコメントとして追記
- **参照必須**:
  - `docs/ai-writing-fixes.md`（品質チェックリスト）
  - `docs/author-persona.md`（ペルソナとの整合確認）
- **完了後**: `content-index.md` の状態を「監査中」→「修正待ち」または「公開準備完了」に更新

---

### 反映チャット

- **目的**: 監査済み・承認済みの記事をブログへ反映する
- **入力**: `content/final/blog/` 内の最終稿
- **作業**:
  - `src/content/blog/` へコピー・配置
  - フロントマター（title / description / pubDate / tags）の最終確認
  - 内部リンク（あわせて読みたい）の確認・追加
  - トップページ（`src/pages/index.astro`）の導線確認
- **完了後**: `content-index.md` の状態を「公開済み」に更新、`status-board.md` から除去

---

### X運用チャット

- **目的**: X（旧Twitter）の投稿文を作成・管理する
- **入力**: 公開済みブログ記事または独自テーマ
- **出力**: `content/drafts/x/` に投稿文ファイルを保存
- **完成後**: `content/final/x/` へ移動し、`content-index.md` を更新
- **運用**:
  - 投稿済みファイルには先頭に投稿日時を記録する
  - `status-board.md` の「X投稿待ち」欄で管理

---

### note運用チャット

- **目的**: noteへの記事を作成・転載・管理する
- **入力**: ブログ記事の転載候補、または独自コンテンツ
- **出力**: `content/drafts/note/` に下書きを保存
- **完成後**: `content/final/note/` へ移動し、`content-index.md` を更新
- **運用**:
  - `status-board.md` の「note候補」欄で候補管理

---

## ID管理ルール

すべてのコンテンツは種別ごとのIDで管理する。

| 種別 | ID形式 | 例 |
|------|--------|-----|
| ブログ記事 | `Bxxx`（3桁） | B001, B012 |
| X投稿 | `Xxxx`（3桁） | X001, X010 |
| note | `Nxxx`（3桁） | N001, N005 |

### ファイル命名規則

`content/drafts/` および `content/final/` 以下のファイルは **ID付きファイル名** を使う。

```
B001-ubuntu-claude-code-setup.md
X001-告知-ubuntu-claude-code.md
N001-ubuntu-ai-kankyo.md
```

- `src/content/blog/` 内の既存ファイル名は **変更しない**（Astroのルーティングに影響するため）
- `content-index.md` の「元ファイル」列と実際のファイル名は必ず一致させる
- 新規IDは `content-index.md` の末尾IDに +1 して採番する

---

## ファイルを正本にする運用ルール

1. **チャット上のテキストは一時的なもの**。完成したら必ずファイルに保存する
2. **下書きは `content/drafts/`** に保存。ファイル名は `Bxxx-スラッグ.md` 形式を使う
3. **最終稿は `content/final/`** に移動してから反映作業を行う
4. **`content-index.md` が唯一の正本一覧**。新規作成・状態変更のたびに更新する
5. **`status-board.md` はダッシュボード**。`content-index.md` と整合性を保つ
6. チャット間でコピペして内容を渡す運用は禁止。ファイルパスを共有する
7. 移行・統合・修正作業は `migration-log.md` に日付付きで記録する

---

## 状態管理ルール

| 状態 | 説明 | 次の状態 |
|------|------|---------|
| 案出し | アイデアのみ。文章未着手 | 下書き |
| 下書き | 文章を作成済み。未レビュー | 監査中 |
| 監査中 | 監査チャットでレビュー中 | 修正待ち / 公開準備完了 |
| 修正待ち | 修正指摘あり。対応が必要 | 下書き（再編集）→ 監査中 |
| 公開準備完了 | レビュー通過。公開・投稿可能 | 公開済み |
| 公開済み | 公開・投稿が完了した状態 | —（アーカイブ） |

---

## ファイル・フォルダ構成

```
content/
  drafts/
    blog/   # ブログ下書き（作業中）
    x/      # X投稿下書き（作業中）
    note/   # note下書き（作業中）
  final/
    blog/   # ブログ最終稿（反映待ち・完成）
    x/      # X投稿最終稿（投稿待ち・完成）
    note/   # note最終稿（公開待ち・完成）

docs/editorial/
  content-index.md  # 全コンテンツの正本一覧
  status-board.md   # 作業優先度ダッシュボード
  workflow.md       # このファイル（運用ルール）
  migration-log.md  # 移行・統合・修正の履歴
  topic-map.md      # SEO構造・テーマ一覧

src/content/blog/   # Astroブログに反映済みの記事
```

---

## 参照ドキュメント一覧

| ファイル | 用途 |
|---------|------|
| `docs/author-persona.md` | 執筆者の人格・価値観定義 |
| `docs/writing-style.md` | 文体ルール・語尾バリエーション |
| `docs/article-template.md` | 記事テンプレート（フロントマター〜締め） |
| `docs/ai-writing-fixes.md` | 品質チェックリスト・リライト指針 |
| `docs/editorial/content-index.md` | 全コンテンツの正本一覧 |
| `docs/editorial/status-board.md` | 作業優先度ダッシュボード |
| `docs/editorial/migration-log.md` | 移行・統合・修正履歴 |
| `docs/editorial/topic-map.md` | SEO構造・テーマ一覧 |
| `CLAUDE.md` | Claude Codeへの全体運用指示 |
