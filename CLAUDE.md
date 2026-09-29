# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## プロジェクト概要

蜘蛛糸まな（Kumoito Mana）のポータルサイト。GitHub Pages でホスティングされる静的サイト。
カスタムドメイン: `kumoito.dev`（CNAME ファイルで設定）

## アーキテクチャ

- **単一ファイル構成**: サイト全体が `index.html` 1ファイルで完成（HTML + CSS + JS をインライン記述）
- **CSS**: `<style>` タグ内の素の CSS。CSS フレームワークは使っていない
- **Google Fonts**: Shippori Mincho B1（見出しの明朝）、Zen Kaku Gothic New（本文）、Cormorant Garamond（欧文の飾り）を `preload` で非同期に読み込み
- **Google Analytics**: `G-FDEZFMDWSK`（gtag.js 経由）
- **ビルドツール**: なし。ビルドステップ不要
- **デプロイ**: `main` ブランチへの push で GitHub Pages に自動デプロイ

## ファイル構成

```
├── index.html              # メインページ（HTML + CSS + JS）
├── CNAME                   # カスタムドメイン設定（kumoito.dev）
├── favicon.png             # ファビコン
├── robots.txt              # クローラー向け設定
├── sitemap.xml             # サイトマップインデックス
├── sitemap-main.xml        # メインサイト用サイトマップ
├── sitemap-grbr-calc.xml   # grbr-calc サービス用サイトマップ
├── sitemap-tier-table-maker.xml  # tier-table-maker サービス用サイトマップ
├── img/                    # 画像アセット
│   ├── hero.png            # ヒーロー背景
│   ├── og.png              # OGP 画像
│   ├── mana001.png, mana002.png  # 立ち絵
│   ├── join-discord.png    # Discord CTA 画像
│   └── *.svg               # SNS・支援サイトアイコン（twitch, youtube, twitter, instagram, fanbox, amazon, buymeacoffee, patreon, github-sponsors）
└── README.md
```

## 開発方法

ビルド・テスト・リントのコマンドはない。ローカル確認は:

```sh
open index.html
```

## index.html の構造

セクションは `<!-- セクション名 - start -->` / `<!-- セクション名 - end -->` コメントで区切られている:
- `hero` - ヒーロー領域（立ち絵 + ナビゲーション + 縦書きの名前 + 右上の蜘蛛の巣）
- `profile` - プロフィール（自己紹介 + 立ち絵画像）
- `services` - 運用しているサービス一覧（`.svc-list` の `<li>` を 1 件ずつ並べる）
- `links` - SNS・支援サイトリンク集（Twitch, YouTube, Twitter, Instagram, pixivFANBOX, Amazon ほしい物リスト, Buy Me a Coffee, Patreon, GitHub Sponsors）
  - 「Twitter」は本人の意向で X に言い換えない
- `discord cta` - Discord サーバー参加 CTA
- `footer` - フッター

### CSS（`<style>` タグ）

デザインは名前の「蜘蛛糸」と Web（蜘蛛の巣）を掛けた和文エディトリアル。色は `:root` の CSS 変数で定義する（和紙 `--paper`、墨 `--ink`、ラベンダー `--lavender`、糸の金 `--gold` など）。
カスタムアニメーション定義: `sway`（ぶら下がる蜘蛛の揺れ）、`draw`（ヒーローの蜘蛛の巣を描く）。いずれも `prefers-reduced-motion: reduce` で止める。
ヒーロー画像（`img/hero.png`、白背景）は `mix-blend-mode: multiply` で和紙色の背景になじませている。

### JavaScript（`<script>` タグ）

- **スクロールアニメーション**: `.reveal` 要素を IntersectionObserver で監視し `.in` クラスを付与
- **蜘蛛の糸**: スクロール量に合わせて `.thread` の `--p` を更新し、左端の蜘蛛が糸を伸ばして降りる
- **蜘蛛の巣の生成**: `webPath()` が放射糸と横糸の SVG パスを作る。ヒーロー右上の `#hero-web` と、リンク集の `#web-svg` の両方で使う
- **リンク集の配置**: `layoutWeb()` が `#web` 内の `.node` を巣の上に並べる。件数と画面幅から、ラベルが重ならない並べ方を `ring`（1 本の輪）→ `stagger`（内外の輪に互い違い）→ `list`（一覧）の順に選び、`#web` の `data-mode` に入れる
- **モバイルメニュー**: `#menu-btn` / `#mobile-menu` / `#menu-close` によるオーバーレイメニュー
- **イースターエッグ**: 左端の蜘蛛（`.thread .spider`）を 8 回（脚の数）続けてつつくと、芥川龍之介『蜘蛛の糸』のように、下から小さな蜘蛛が登ってきて糸が切れ、全員が落ちたあと新しい糸で蜘蛛が降りてくる。演出用の要素は `.egg` にまとめて一時的に追加し、終わったら消す。演出中はスクロールによる蜘蛛の位置の更新（`threadFrozen`）を止め、最後に蜘蛛が降りてくるときに、その時点のスクロール位置へ戻す。`prefers-reduced-motion: reduce` のときは台詞だけを出す

### リンクやサービスを増減するとき

- 各種リンクは `#web` 内の `<a class="node">` を 1 行足すか消すだけでよい。位置は `layoutWeb()` が自動で決め、HTML の並び順に真上から時計回りに置かれる。アイコンは `img/` に SVG を置いて `<span class="dot">` の中で参照する
- サービスは `.svc-list` に `<li class="reveal">` を 1 件足す。番号（`01`〜）は手で振っているので、並べ替えたら振り直す

## 注意事項

- OGP / Twitter Card メタタグの URL は `https://kumoito.dev/` を使用。ドメインや画像パスの変更時は `og:url`, `og:image`, `canonical`, `twitter:site`, `twitter:creator` をすべて合わせて更新すること
- `CNAME` ファイルはカスタムドメイン（`kumoito.dev`）に必須。削除・変更するとサイトが `*.github.io` に戻るため注意
- コミットメッセージは日本語で書く
- 外部リンク（SNS URL、Discord 招待リンク等）は本人の実アカウントなので、変更時は必ず確認を取ること
- 外部リンクには必ず `target="_blank" rel="noopener noreferrer"` を付与すること
- `sitemap.xml` はサイトマップインデックス形式。新サービス追加時は個別サイトマップ（`sitemap-{service}.xml`）を作成し、`sitemap.xml` に `<sitemap>` エントリを追加すること
- `robots.txt` は `sitemap.xml` を参照している。サイトマップのパスを変更した場合は `robots.txt` も更新すること
