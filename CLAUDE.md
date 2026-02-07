# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## プロジェクト概要

蜘蛛糸まな（Kumoito Mana）のポータルサイト。GitHub Pages でホスティングされる静的サイト。
カスタムドメイン: `kumoito.dev`（CNAME ファイルで設定）

## アーキテクチャ

- **単一ファイル構成**: サイト全体が `index.html` 1ファイルで完成している（HTML + CSS + JavaScript をインライン記述）
- **CSS フレームワーク**: Tailwind CSS を CDN (`cdn.tailwindcss.com`) 経由で使用。カスタム設定は `<script>` タグ内の `tailwind.config` で定義
- **ビルドツール**: なし。ビルドステップ不要で、ファイルを直接編集してデプロイ
- **デプロイ**: `main` ブランチへの push で GitHub Pages に自動デプロイ

## 開発方法

ビルド・テスト・リントのコマンドはない。ブラウザで `index.html` を直接開いて確認する。

## ファイル構成

- `index.html` - サイト本体（HTML/CSS/JS すべて含む）
- `CNAME` - カスタムドメイン設定
- `favicon.png` - ファビコン画像
- `img/` - 画像アセット（ヒーロー画像、立ち絵、OGP画像、SNS アイコン SVG）

## index.html の構造

セクションは HTML コメントで区切られている:
- `<!-- hero -->` - ヒーロー領域（背景画像 + ナビゲーション + キャッチコピー）
- `<!-- profile -->` - プロフィール（自己紹介 + 立ち絵画像）
- `<!-- links -->` - SNS リンク集（Twitch, YouTube, Twitter, Instagram, Fanbox, Amazon）
- `<!-- discord cta -->` - Discord サーバー参加 CTA
- `<!-- footer -->` - フッター

`<style>` タグ内にカスタム CSS アニメーション（gradient-shift, float, pulse-glow, text-glow 等）を定義。
`<script>` タグ内に IntersectionObserver によるスクロールアニメーション、パララックス効果、カーソルエフェクト、テキストスクランブル効果を実装。

## 注意事項

- OGP メタタグのURL は `https://kumoito.dev/` を使用。変更時は合わせて更新すること
- コミットメッセージは日本語で書かれている
