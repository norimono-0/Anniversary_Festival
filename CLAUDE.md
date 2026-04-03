## Overview

静的な単一ページのお祝い演出サイト。祝うアニメーション付き賞状ページ。
スマホでQRコードを読み取ることで演出が発動する想定。

## Development

ビルドツール・パッケージマネージャなし。`index.html` をブラウザで直接開くだけで動作する。

```bash
# ローカルで確認する場合（任意）
python3 -m http.server 8080
# → http://localhost:8080 にアクセス
```

## Architecture

ファイル構成: `index.html` + `image.png` + `qr.html`（QRコード表示ページ）

**3段階のアニメーションシーケンス（自動再生）:**

1. **STEP 1 – 賞状表示** (`#classic-award`): `image.png` を背景画像として使用した賞状が浮き上がるアニメーション
2. **STEP 2 – エディタ表示** (`#editor-container`): コードがタイプライター風に入力される演出（`verification.js` 風のダークテーマエディタ）
3. **STEP 3 – 最終画面** (`#final-screen`): 「おめでとう！」メッセージとキラキラ（Canvas）アニメーション + 「← RESTART」ボタンで STEP 1 に戻れる

**リセット機能:**
- 最終画面の `← RESTART` ボタン（`resetToStart()`）でアニメーション全体を最初から再生できる
- スパークルアニメーションは `sparkleActive` フラグで停止制御

**外部依存（CDN）:**
- Tailwind CSS (`cdn.tailwindcss.com`)
- Google Fonts: `Noto Serif JP`（賞状文字）、`Fira Code`（エディタ表示）

## Customization Points

受賞者名や文言を変更する場合、以下の2箇所を編集する:
- `index.html:159-161` – 最終画面の受賞者名・メッセージ（`笹川 太郎 殿` など）
- `index.html:209-212` – エディタ内のコード文字列 `achievement` オブジェクト（`recipient`, `certification`, `issued_at`）

## Deployment

**公開URL:** `https://norimono-0.github.io/Anniversary_Festival/`

1. `main` ブランチへ push
2. GitHub リポジトリ（`norimono-0/Anniversary_Festival`）の Settings → Pages → Branch: `main` / root を設定
3. `qr.html` にアクセスして QR コードを取得・印刷
