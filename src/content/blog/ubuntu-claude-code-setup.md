---
title: 'UbuntuにClaude Codeを導入してAI作業環境を整える手順'
description: 'UbuntuにClaude Codeを導入し、AI作業環境を整えるまでの手順をまとめた記事'
pubDate: '2026-03-08'
tags: ["Ubuntu", "Claude Code", "AI作業環境"]
---

## はじめに

Ubuntuを使い始めてしばらくたったころ、AI支援のツールを試してみたくなりました。
調べるうちにClaude Codeというターミナルで動くAIツールにたどり着き、実際に導入してみました。
設定のつまずきポイントも含めて、実際の手順をこの記事にまとめています。
同じ環境を整えようとしている方の参考になれば幸いです。

## 前提環境

この記事では以下の環境を前提にしています。

- OS：Ubuntu 24.04 LTS
- Node.js：v18以上（`node -v` で確認できます）
- npm：Node.jsに同梱されているものを使用

Node.jsがまだ入っていない場合は、`nvm`（Node Version Manager）を使ってインストールするのが楽です。
ターミナルの基本操作（コマンドの入力、ディレクトリの移動など）ができれば、特別な知識は必要ありません。

## Claude Codeのインストール

npmを使ってClaude Codeをグローバルインストールします。

```bash
npm install -g @anthropic-ai/claude-code
```

インストール後、`claude` コマンドが使えるようになります。
もし `command not found` と表示される場合は、npmのグローバルインストール先にPATHが通っていない可能性があります。
`npm bin -g` でパスを確認し、`.bashrc` や `.zshrc` に追記することで解決できます。
再起動後、または `source ~/.bashrc` を実行すると反映されます。

## 初期設定

初回起動時に `claude` と入力すると、AnthropicのAPIキーの入力を求められます。
APIキーはAnthropicのコンソール画面から取得できます（アカウント登録が必要です）。
認証が完了すると、ターミナル上でClaude Codeが使えるようになります。

プロジェクトごとに `CLAUDE.md` というファイルをルートに置いておくと、そのプロジェクトのコンテキストをClaude Codeに伝えられて便利です。
たとえば「このブログはAstroで作っています」「使用言語は日本語です」といった情報を書いておくと、やり取りがスムーズになります。

## まとめ

Ubuntu上でのClaude Codeの導入は、npmでのインストールとAPIキーの設定という2ステップで完了します。
PATHの設定だけ少し注意が必要ですが、一度通してしまえばあとは普通に使えます。
ターミナルからAIと対話しながら作業できる環境は、思っていたよりずっと便利です。
今後はClaude Codeを使った実際の作業例なども記事にまとめていく予定です。

---

## あわせて読みたい

- [Ubuntu導入後に最初に入れておくと便利なツール](/blog/ubuntu-first-tools)
- [Claude Codeを使う前に決めておくべき作業ルール](/blog/claude-code-work-rules)
