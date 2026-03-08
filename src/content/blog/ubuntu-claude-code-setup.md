---
title: 'UbuntuにClaude Codeを導入してAI作業環境を整える手順'
description: 'UbuntuにClaude Codeを導入し、AI作業環境を整えるまでの手順をまとめた記事'
pubDate: '2026-03-08'
sortOrder: 1
tags: ["Ubuntu", "Claude Code", "AI作業環境"]
---

## はじめに

Ubuntuを使い始めてしばらくたったころ、ターミナルで動くAIツール「Claude Code」を導入しました。インストール自体は短い時間で終わりますが、PATH設定やAPIキーの取得でつまずきやすいポイントがいくつかあります。この記事では「そのまま順番に進めれば導入できる」ことを目指して、手順をできるだけ具体的にまとめています。各コマンドはコードブロック右上の「コピー」ボタンでそのままコピーできます。Ubuntuでこのページを開き、ターミナルでCtrl+Shift+Vを押して貼り付けると手入力の必要がありません。

---

## 前提環境

- OS：Ubuntu 22.04 / 24.04 LTS
- ターミナル（端末）を開ける状態であること
- Node.js v18以上（このあとの手順でインストールします）

「ターミナル」とは、Ubuntuの黒い画面でコマンドを入力する場所です。アプリ一覧から「端末」または「Terminal」を探して開いてください。

---

## ステップ1：Node.jsをインストールする

Claude Codeを動かすには Node.js（バージョン18以上）が必要です。`nvm`（Node Version Manager）を使うと、PATHの設定も自動で整うためおすすめです。

ターミナルに以下を**1行ずつ**貼り付けてEnterを押してください。

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
```

```bash
source ~/.bashrc
```

```bash
nvm install --lts
```

```bash
nvm use --lts
```

完了したら、正しくインストールされたか確認します。

```bash
node -v
```

`v22.x.x` のようなバージョン番号が表示されれば成功です。

---

## ステップ2：Claude Codeをインストールする

次のコマンドを1行そのまま貼り付けてEnterを押してください。

```bash
npm install -g @anthropic-ai/claude-code
```

少し時間がかかります（1〜3分程度）。完了したら動作確認をします。

```bash
claude --version
```

バージョン番号が表示されればインストール完了です。

---

## ステップ3：APIキーを取得する

Claude Codeを使うには、AnthropicのAPIキーが必要です。APIキーはAnthropicの**コンソール画面**から取得します。

> **注意：**「claude.ai」（チャット画面）とは別の管理画面です。claude.aiにログインしていても、APIキーの取得にはコンソール画面への別途アクセスが必要です。

手順は次の通りです。

1. ブラウザで `console.anthropic.com` を開く
2. アカウントがなければ「Sign up」でメールアドレス登録・確認をする
3. ログイン後、左メニューまたは設定画面の中から「API Keys」を探す
4. 「Create Key」（または「+ New Key」）ボタンをクリックする
5. キーの名前を何か入力して作成する（例：`ubuntu-work`）
6. 表示された文字列（`sk-ant-` で始まる長い文字列）をそのままコピーする

> **重要：**APIキーはこの画面を閉じると二度と表示されません。必ずコピーしてから閉じてください。コピーし忘れた場合は、そのキーを削除して新しく作成すれば問題ありません。

---

## ステップ4：Claude Codeを起動・認証する

ターミナルで次のコマンドを入力します。

```bash
claude
```

初回起動時にAPIキーの入力を求められます。先ほどコピーした `sk-ant-` で始まる文字列を貼り付けてEnterを押してください。

認証が完了すると、ターミナル上でClaude Codeとやり取りできる状態になります。試しに「こんにちは」と入力してみてください。

---

## よくあるつまずきポイント

### `claude: command not found` と表示される

インストールは成功しているのに `claude` が使えない場合、PATHが通っていないことが多いです。`nvm` を使った場合はこの問題は起きにくいですが、システムのnpmを使った場合に起きることがあります。以下を実行してみてください。

```bash
echo 'export PATH="$HOME/.npm-global/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
claude --version
```

それでも解決しない場合は、グローバルインストール先を確認します。

```bash
npm config get prefix
```

表示されたパスに `/bin` を足した場所（例：`/usr/local/bin`）がインストール先です。このパスを上記の `export PATH=` の部分に合わせて書き換えてください。

### コマンドをどこに貼ればいいか分からなくなる

「ターミナル（端末）」アプリを開いて、カーソルが点滅している行に貼り付けてEnterを押すだけです。コマンドを貼る場所に迷った場合は、一度ターミナルを閉じて開き直すと初期状態に戻ります。

### APIキーの取得画面が見つからない

`claude.ai`（チャット画面）にはAPIキーの取得機能はありません。必ず `console.anthropic.com` をブラウザで直接開いてください。ログインしたあと、画面左のメニューに「API Keys」が見当たらない場合は、画面上部のアカウントメニューや「Settings」の中を探してみてください。

### 英語の画面が多くて手が止まる

コンソール画面はほぼ英語ですが、操作する項目は限られています。「API Keys」「Create Key」「Copy」の3つが見つかれば、あとはほぼ日本語の説明通りに進められます。エラーメッセージが出た場合は、そのまま翻訳ツールにコピーすると内容が分かりやすくなります。

---

## CLAUDE.mdを作っておくと便利

プロジェクトのフォルダに `CLAUDE.md` というファイルを置いておくと、Claude Codeがそのプロジェクトの情報を把握した状態で作業してくれます。内容は自由ですが、たとえば次のように書いておくだけで変わります。

```
# このプロジェクトについて
- 言語：日本語で書く
- フレームワーク：Astro
- 目的：Ubuntu×AIブログの運営
```

作成方法はターミナルで次のように入力するだけです（プロジェクトのフォルダで実行してください）。

```bash
nano CLAUDE.md
```

内容を書いてCtrl+Oで保存、Ctrl+Xで閉じます。

---

## まとめ

Claude Codeの導入はNode.jsのインストール、Claude Codeのインストール、APIキーの取得と設定の3ステップで完了します。PATHの問題とAPIキーの取得場所の2点でつまずきやすいですが、この記事の手順通りに進めれば対応できます。導入後の使い方や作業ルールの考え方については「[Claude Codeを使う前に決めておくべき作業ルール](/blog/claude-code-work-rules)」も参考になります。

---

## あわせて読みたい

- [Claude Codeを使う前に決めておくべき作業ルール](/blog/claude-code-work-rules)
- [Claude Codeでどこまで自動化できるか](/blog/claude-code-automation-limits)
- [Ubuntu導入後に最初に入れておくと便利なツール](/blog/ubuntu-first-tools)
- [AI作業環境を整えるときにパスワード管理を先に決めた方がいい理由](/blog/password-management-for-ai-tools)
