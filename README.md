# 蜘蛛糸まなポータル

蜘蛛糸まな（Kumoito Mana）のポータルサイトです。

🌐 **https://kumoito.dev**

## 概要

Ruby on Rails エンジニア / VTuber 蜘蛛糸まなの配信・SNS・コミュニティへのリンク集ポータルサイトです。

## 技術スタック

- HTML / CSS / JavaScript（単一ファイル構成、CSS フレームワークなし）
- Google Fonts（Shippori Mincho B1 / Zen Kaku Gothic New / Cormorant Garamond）
- GitHub Pages（ホスティング）

## ファイル構成

```
├── index.html     # サイト本体（HTML/CSS/JS すべて含む）
├── CNAME          # カスタムドメイン設定
├── robots.txt     # クローラー向け設定（sitemap 参照を含む）
├── sitemap.xml    # sitemap index（全体入口）
├── sitemap-main.xml # ルート配下ページ用 sitemap
├── sitemap-tier-table-maker.xml # tier-table-maker 用 sitemap
├── sitemap-grbr-calc.xml # grbr-calc 用 sitemap
├── favicon.png    # ファビコン
└── img/           # 画像アセット
    ├── hero.png        # ヒーロー背景画像
    ├── mana001.png     # 立ち絵
    ├── mana002.png     # 立ち絵
    ├── og.png          # OGP 画像
    ├── join-discord.png # Discord CTA 画像
    └── *.svg           # SNS アイコン
```

## 開発

ビルドツール不要です。`index.html` をブラウザで直接開いて確認できます。

```sh
open index.html
```

## デプロイ

`main` ブランチへの push で GitHub Pages に自動デプロイされます。

## Search Console / SEO 運用メモ

- Search Console は `kumoito.dev` の Domain プロパティを主に運用する（DNS TXT 検証を推奨）。
- サービス単位の可視化が必要な場合は、補助的に URL プレフィックスを追加する。
  - `https://kumoito.dev/tier-table-maker/`
  - `https://kumoito.dev/grbr-calc/`
- `robots.txt` は `https://kumoito.dev/sitemap.xml`（sitemap index）を参照する。
- sitemap index は以下を集約する。
  - `https://kumoito.dev/sitemap-main.xml`
  - `https://kumoito.dev/sitemap-tier-table-maker.xml`
  - `https://kumoito.dev/sitemap-grbr-calc.xml`
- サービス配下（`/tier-table-maker/`, `/grbr-calc/`）は各アプリのデプロイで上書きされうるため、sitemap はルート配下で管理する。
