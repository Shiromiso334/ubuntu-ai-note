# X004 B017 告知X下書き作成 task

## 基本情報

- **Task ID**: T260314-01
- **対象コンテンツID**: X004
- **担当**: Claude Code
- **依頼元**: Codex
- **優先度**: 中
- **承認モード**: auto

## 目的

公開済みブログ記事 B017 の告知用 X 投稿文を作成し、人間確認待ちまで進める。

## 背景

- 対象ブログ記事: Ubuntuインストール直後に最初に確認したい初回セットアップ項目
- 記事URL: https://www.ubuntu-ai-note.com/blog/ubuntu-first-setup/
- 媒体は X（旧Twitter）
- 誇張せず、初心者に伝わる短文でまとめる

## 作業対象

- **対象ファイル**:
  - `content/drafts/x/X004-ubuntu-first-setup-announce.md`
- **参照ファイル**:
  - `src/content/blog/ubuntu-first-setup.md`
  - `docs/content-channels.md`
  - `docs/author-persona.md`
  - `docs/editorial/content-index.md`
  - `docs/editorial/status-board.md`
- **更新してよいファイル**:
  - `content/drafts/x/X004-ubuntu-first-setup-announce.md`
  - `docs/editorial/content-index.md`
  - `docs/editorial/status-board.md`
  - `logs/260314-01-x004-ubuntu-first-setup-announce.md`

## 実施内容

1. ブログ記事を読み、X 用の告知文を 1案作成する
2. `content/drafts/x/X004-ubuntu-first-setup-announce.md` に保存する
3. `content-index.md` の X004 を `公開準備完了`、担当 `Human`、次アクション `人間確認後に投稿` に更新する
4. `status-board.md` の `X投稿待ち` に X004 を追加する
5. 実施ログを `logs/260314-01-x004-ubuntu-first-setup-announce.md` に保存する

## 完了条件

- X 投稿文が 1本保存されている
- X004 が人間確認待ち相当の状態に更新されている
- `status-board.md` の `X投稿待ち` に反映されている

## 停止条件

- 記事内容から X 投稿の訴求点が判断しにくい
- 外部投稿や予約操作が必要になった

## 検証

- 140字前後に収まっているか確認する
- 記事 URL が入っているか確認する

## 出力

- 更新ファイル一覧
- 投稿文
- 人間への確認事項
