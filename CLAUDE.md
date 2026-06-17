# 献立提案ナビ — エージェント指示書

## プロジェクト概要
スーパーマーケット向けの献立提案アプリ。  
GitHub Pages でホスティング: `https://supervalue-hh.github.io/kondate-navi/`  
リポジトリ: `https://github.com/supervalue-hh/kondate-navi`

## ファイル構成
- `index.html` — アプリ本体（単一ファイル）
- `robots.txt` — 検索エンジンをブロック（変更不要）

## 編集・デプロイ手順

### 1. 変更する
`index.html` のみ編集する。

### 2. デプロイする
編集後は以下を実行してください:

```powershell
cd "C:\Users\h.hamano\Documents\kondate-navi"
git add index.html
git commit -m "<変更内容を一言で>"
git push
```

デプロイ後、GitHub Pages への反映は数分かかります。

## アーキテクチャ

### データ形式（RDB 配列）
```
[名前, 時間ラベル, 難易度ラベル, 食材[], 手順[], time_tag, mood_tags[], scene_tag, flavor_tag, diff_tag]
```
- `r[5]` time_tag: `'speed'`(〜15分) / `'medium'`(20〜30分) / `'slow'`(40分〜)
- `r[6]` mood_tags[]: `'tired'` / `'energetic'` / `'warm'` / `'healthy'`
- `r[7]` scene_tag: `'self'` / `'family'` / `'guest'`
- `r[8]` flavor_tag: `'j'`(和風) / `'w'`(洋風) / `'c'`(中華・アジア)
- `r[9]` diff_tag: `'easy'` / `'normal'` / `'hard'`

### フィルタ優先度（scene は絶対に外さない）
1. 全条件一致
2. diff を外す
3. diff + mood を外す
4. diff + mood + flavor を外す（scene は常に保持）

### 画面構成
- `s1`: トップ（時間選択 + おまかせボタン + 記念日）
- `s2`: 気分
- `s3`: シーン
- `s4`: 味付け
- `s5`: 難易度
- `s6`: 結果一覧
- `s7`: レシピ詳細（QRコード付き）
- `s8`: 記念日カレンダー

## 注意事項
- 金額表示は廃止済み（追加しないこと）
- `healthy` タグは野菜・豆腐中心の料理のみ（うどん・チャーハンなどに付けない）
- QRコードはレシピ名でGoogle検索するURLを生成
