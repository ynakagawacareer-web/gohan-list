# 近所のごはん屋 — セットアップ手順

ログイン不要・無料で家族全員が使えるアプリです。  
所要時間：約15分

---

## ファイル構成

```
index.html   ← アプリ本体
gas_code.js  ← Googleスプレッドシート用サーバーコード
README.md    ← この手順書
```

---

## STEP 1｜Googleスプレッドシートを作る

1. https://sheets.google.com を開く
2. 「空白のスプレッドシート」を作成（名前は何でもOK）

---

## STEP 2｜Google Apps Script を設定する

1. スプレッドシートのメニュー「**拡張機能**」→「**Apps Script**」
2. エディタの中身を全部消す
3. `gas_code.js` の中身を全部コピーして貼り付け
4. Ctrl+S で保存
5. 「**デプロイ**」→「**新しいデプロイ**」
6. 歯車アイコン ⚙ →「**ウェブアプリ**」を選択
7. アクセスできるユーザー：**「全員」**
8. 「**デプロイ**」をクリック
9. 承認画面が出たら：「アクセスを承認」→アカウント選択→「詳細」→「〜に移動」→「許可」
10. 表示された `https://script.google.com/macros/s/xxx/exec` 形式のURLをコピー

---

## STEP 3｜index.html にURLを貼る

`index.html` をテキストエディタで開き、以下の行を探して書き換える：

```
const GAS_URL = "YOUR_GAS_URL_HERE";
```
↓
```
const GAS_URL = "https://script.google.com/macros/s/xxxxxxx/exec";
```

保存後、`index.html` をブラウザで開いてお店を1件追加→スプレッドシートに反映されれば成功。

---

## STEP 4｜GitHub Pages で公開する

1. https://github.com でアカウント作成（無料）
2. 「＋」→「New repository」→名前を入力→**Public**→「Create repository」
3. GitHub Desktop をインストール（https://desktop.github.com）
4. 「File」→「Clone repository」でリポジトリをローカルに複製
5. `index.html` をそのフォルダにコピー
6. GitHub Desktop で「Commit to main」→「Push origin」
7. GitHubのリポジトリページ「Settings」→「Pages」→Branch を **main** に設定→「Save」
8. 数分後に `https://あなたのID.github.io/リポジトリ名/` でアクセス可能

---

## STEP 5｜家族に共有する

発行されたURLをLINEで送るだけ。  
**家族側はGoogleアカウントもGitHubアカウントも不要。**

---

## 修正・メンテの手順

1. Claudeに修正を依頼 → `index.html` をダウンロード
2. `gohan-list` フォルダに上書き保存
3. GitHub Desktop で：
   - **Fetch origin**（他のPCの変更を取り込む）
   - コメント入力 →「**Commit to main**」
   - 「**Push origin**」

複数PCから編集する場合は毎回 **Fetch origin** から始める。

---

## 機能一覧

- 食べログのコピペから店名・住所・URLを自動抽出
- 訪問済みフラグ（チェックで切り替え）
- 一言メモ
- 絞り込み（すべて・まだ行ってない・行った！）
- ソート（登録順・店名順・住所順）
- 重複登録防止
- 削除時の確認UI
- 家族全員がリアルタイムで共有・編集可能

---

## トラブルシューティング

**お店が追加できない**  
→ GAS_URLの末尾に `/exec` がついているか確認。

**スプレッドシートに反映されない**  
→ GASを「デプロイを管理」→「編集」→「新バージョン」で再デプロイ。

**「アクセスを承認」画面でエラー**  
→「詳細」→「安全でないページに移動」→「許可」の順に進む。
