# 近所のごはん屋 — Cowork引き継ぎメモ

## プロジェクト概要

家族で共有する近所の飲食店リストアプリ。  
ブラウザで動くHTMLファイル1枚 + Google Apps Scriptで構成。

---

## ファイル構成

- **index.html** — アプリ本体（これをGitHub Pagesで公開）
- **gas_code.js** — Googleスプレッドシート用APIサーバー
- **README.md** — セットアップ手順

---

## 環境情報

| 項目 | 内容 |
|------|------|
| GitHub リポジトリ | https://github.com/ynakagawacareer-web/gohan-list |
| 公開URL | https://ynakagawacareer-web.github.io/gohan-list/ |
| GAS URL | https://script.google.com/macros/s/AKfycbyPRzoNIqVTcZcNIiXkDPcnVA53XqxZrR0ahQcOU9aEFkccyjNGJRjy2Gk5XASKWLkm/exec |
| データ保存先 | Googleスプレッドシート（GAS経由） |

---

## 実装済み機能

- 食べログのコピペ（店名・電話・住所・URL）から自動抽出して登録
- 訪問済みフラグ（チェックボタンで切り替え、緑カードに変化）
- 一言メモ（追加時・編集時に入力可）
- 絞り込み（すべて・まだ行ってない・行った！）
- ソート（登録順新しい順・登録順古い順・店名順・住所順）※デフォルトは登録順古い順
- 重複登録防止（URLまたは店名で判定、警告表示＋追加ボタン無効化）
- 削除確認UI（カード内インライン表示）
- 統計表示（登録店舗数・行ったお店・まだのお店）
- レスポンシブ対応（スマホでも使える）

---

## データ構造（スプレッドシートの列）

| 列 | フィールド | 内容 |
|----|-----------|------|
| A | id | タイムスタンプ（Date.now()） |
| B | name | 店名 |
| C | url | 食べログURL |
| D | visited | 訪問済みフラグ（true/false） |
| E | createdAt | 登録日 |
| F | address | 住所 |
| G | memo | 一言メモ |

---

## デザイン仕様

- **背景色：** #FAF7F2（オフホワイト）
- **メインカラー：** #C0392B（深い赤）
- **訪問済みカラー：** #4A7C59（グリーン）
- **フォント：** Noto Serif JP（見出し）、Noto Sans JP（本文）
- **カードスタイル：** 白背景・角丸・ホバーで赤枠

---

## 修正作業の手順

1. GitHub Desktopで **Fetch origin**（他PCの変更を取り込む）
2. Claudeに修正内容を伝える
3. 生成された `index.html` をローカルの `gohan-list` フォルダに上書き保存
4. GitHub Desktopで **Commit to main** → **Push origin**

---

## 今後やりたいこと（未実装）

- Google Mapsで登録店舗をピン表示する機能
