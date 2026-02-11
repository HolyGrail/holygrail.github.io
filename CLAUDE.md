# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## プロジェクト概要

蜘蛛糸まな（Kumoito Mana）のポータルサイト。GitHub Pages でホスティングされる静的サイト。
カスタムドメイン: `kumoito.dev`（CNAME ファイルで設定）

## アーキテクチャ

- **単一ファイル構成**: サイト全体が `index.html` 1ファイルで完成（HTML + CSS + JS をインライン記述）
- **Tailwind CSS**: CDN (`cdn.tailwindcss.com`) 経由。カスタム設定は `tailwind.config` オブジェクトで定義（フォント: Inter + Noto Sans JP、fade-in / slide-up アニメーション）
- **Google Fonts**: Inter（英文）と Noto Sans JP（和文）を `preload` で読み込み
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
│   └── *.svg               # SNS アイコン（twitch, youtube, twitter, instagram, fanbox, amazon）
└── README.md
```

## 開発方法

ビルド・テスト・リントのコマンドはない。ローカル確認は:

```sh
open index.html
```

## index.html の構造

セクションは `<!-- セクション名 - start -->` / `<!-- セクション名 - end -->` コメントで区切られている:
- `hero` - ヒーロー領域（背景画像 + ナビゲーション + キャッチコピー）
- `profile` - プロフィール（自己紹介 + 立ち絵画像）
- `links` - SNS リンク集（Twitch, YouTube, Twitter, Instagram, Fanbox, Amazon）
- `discord cta` - Discord サーバー参加 CTA
- `footer` - フッター

### CSS（`<style>` タグ）

カスタムアニメーション定義: `gradient-shift`, `float`, `pulse-glow`, `text-glow`, `slide-in-right`, `reveal-up`, `hero-image-pan`。
カラーテーマは紫系グラデーション（`#667eea` → `#764ba2` → `#f093fb` → `#4facfe`）で統一。

### JavaScript（`<script>` タグ）

- **スクロールアニメーション**: `.observe-fade` 要素を IntersectionObserver で監視し `.reveal-animated` クラスを付与
- **パララックス**: ヒーロー背景画像のスクロール連動
- **カーソルエフェクト**: `#cursor-glow` 要素がマウスに追従
- **テキストスクランブル**: `TextScramble` クラスで h1/h2 ホバー時にグリッチ風効果
- **モバイルメニュー**: `#mobile-menu-btn` / `#mobile-menu` によるオーバーレイメニュー
- **マグネティックボタン**: `.magnetic-button` 要素がマウス位置に引き寄せられる効果

## 注意事項

- OGP / Twitter Card メタタグの URL は `https://kumoito.dev/` を使用。ドメインや画像パスの変更時は `og:url`, `og:image`, `canonical`, `twitter:site`, `twitter:creator` をすべて合わせて更新すること
- `CNAME` ファイルはカスタムドメイン（`kumoito.dev`）に必須。削除・変更するとサイトが `*.github.io` に戻るため注意
- コミットメッセージは日本語で書く
- 外部リンク（SNS URL、Discord 招待リンク等）は本人の実アカウントなので、変更時は必ず確認を取ること
- 外部リンクには必ず `target="_blank" rel="noopener noreferrer"` を付与すること
- `sitemap.xml` はサイトマップインデックス形式。新サービス追加時は個別サイトマップ（`sitemap-{service}.xml`）を作成し、`sitemap.xml` に `<sitemap>` エントリを追加すること
- `robots.txt` は `sitemap.xml` を参照している。サイトマップのパスを変更した場合は `robots.txt` も更新すること
