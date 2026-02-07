# 蜘蛛糸まなポータル

蜘蛛糸まな（Kumoito Mana）のポータルサイトです。

🌐 **https://kumoito.dev**

## 概要

Ruby on Rails エンジニア / VTuber 蜘蛛糸まなの配信・SNS・コミュニティへのリンク集ポータルサイトです。

## 技術スタック

- HTML / CSS / JavaScript（単一ファイル構成）
- [Tailwind CSS](https://tailwindcss.com/)（CDN 経由）
- GitHub Pages（ホスティング）

## ファイル構成

```
├── index.html     # サイト本体（HTML/CSS/JS すべて含む）
├── CNAME          # カスタムドメイン設定
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
