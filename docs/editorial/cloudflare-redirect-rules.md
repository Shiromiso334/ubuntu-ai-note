# Cloudflare Redirect Rules メモ

`ubuntu-ai-note.com` の正規URLは `https://www.ubuntu-ai-note.com/` に統一する。
Search Console の重複URL対策として、Cloudflare 側で host 正規化を入れる。

## 目的

- `http://ubuntu-ai-note.com/` を `https://www.ubuntu-ai-note.com/` へ統一
- `http://www.ubuntu-ai-note.com/` を `https://www.ubuntu-ai-note.com/` へ統一
- `https://ubuntu-ai-note.com/` を `https://www.ubuntu-ai-note.com/` へ統一

## 推奨ルール

Cloudflare Dashboard:

- `Rules`
- `Redirect Rules`
- `Create rule`

### Rule name

`force-www-https`

### If incoming requests match

Custom filter expression:

```txt
(http.host eq "ubuntu-ai-note.com") or (http.request.scheme eq "http")
```

### Then

Dynamic Redirect

Target URL:

```txt
concat("https://www.ubuntu-ai-note.com", http.request.uri.path)
```

Preserve query string:

`On`

Status code:

`301`

## 注意

- すでに別の host / scheme リダイレクトがある場合は競合しない順序にする
- `www` が正規でない運用に変えるなら、`astro.config.mjs` の `site` も合わせて変える
- 反映後は以下を確認する
  - `http://ubuntu-ai-note.com/`
  - `http://www.ubuntu-ai-note.com/`
  - `https://ubuntu-ai-note.com/`
  - すべて `https://www.ubuntu-ai-note.com/` に 301 されること

## Search Console での確認

Cloudflare 反映後に以下を行う。

1. `https://www.ubuntu-ai-note.com/robots.txt` が正常か確認
2. `https://www.ubuntu-ai-note.com/sitemap-index.xml` を再送信
3. 重複URLエラーとリダイレクトエラーで `修正を検証`
