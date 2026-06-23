---
name: wiki-article-html
description: >-
  Convert plain-text data into consistent, semantic HTML/CSS web articles such as
  game strategy wiki pages. Use when the user provides plain text and asks to build,
  format, or convert it into an article, wiki page, 記事, or 攻略Wiki page, or whenever
  raw article data is passed without a specified format.
---

# Wiki Article HTML Builder

プレーンテキストのデータを、一貫したデザインのWeb記事（攻略Wiki用ページなど）へ変換するためのスキル。以下のルールは**厳格に**守ること。

## AIの振る舞い（最重要）

今後ユーザーからプレーンテキストのデータが渡された際は、出力形式の指示がなくても**このルールに従って自動的に適切なHTML構造へ変換し、完成したコードを出力する**こと。曖昧なデータでも、見出し・箇条書き・表・強調枠へ妥当に振り分けて構造化する。

## 厳格なルール

### 1. HTML構造（セマンティックHTML5）
- 記事全体は必ず `<article>` で囲む。
- 論理的なまとまりごとに必ず `<section>` で区切る。
- タイトル・導入部には必ず `<header>` を使用する。
- `<div>` の多用を避け、意味に合うタグ（`<table>`, `<ul>`, `<figure>` 等）を優先する。

### 2. クラス命名規則（BEM記法）
- すべてのクラス名は BEM（`Block__Element--Modifier`）をベースにする。
- Block はコンポーネント名（例: `article`, `callout`, `data-table`）。
- Element は `__` で連結（例: `article__heading`）。
- Modifier は `--` で連結（例: `callout--warning`）。
- スネーク/キャメル混在を避け、Block・Elementはケバブケース（小文字+ハイフン）で統一する。

### 3. 必須コンポーネント（標準構成）
すべての記事に以下を**標準で組み込む**こと。該当データが無い場合のみ省略可。

1. 見出し: `<h2>`（大見出し）と `<h3>`（小見出し）で階層化する。
2. 特徴の箇条書き: `<ul>` / `<li>` を使う。
3. データ比較用の表: `<table>`（`<thead>` / `<tbody>` を含む）を使う。
4. 重要事項の強調枠: 専用の callout ブロックで囲む。

## 出力テンプレート

完全なHTML骨格・CSS・BEMクラス一覧・変換例は [reference.md](reference.md) を参照し、それに沿って出力する。

基本骨格は以下:

```html
<article class="wiki-article">
  <header class="wiki-article__header">
    <h1 class="wiki-article__title">記事タイトル</h1>
    <p class="wiki-article__lead">導入文</p>
  </header>

  <section class="wiki-article__section">
    <h2 class="wiki-article__heading">大見出し</h2>
    <h3 class="wiki-article__subheading">小見出し</h3>
    <p class="wiki-article__text">本文</p>

    <ul class="feature-list">
      <li class="feature-list__item">特徴1</li>
    </ul>

    <table class="data-table">
      <thead>
        <tr><th class="data-table__head">項目</th><th class="data-table__head">値</th></tr>
      </thead>
      <tbody>
        <tr><td class="data-table__cell">A</td><td class="data-table__cell">100</td></tr>
      </tbody>
    </table>

    <aside class="callout callout--warning">
      <p class="callout__title">注意</p>
      <p class="callout__text">重要事項</p>
    </aside>
  </section>
</article>
```

## 出力ワークフロー

1. 受け取ったテキストを論理ブロックへ分解する（導入 / 各トピック / データ / 注意点）。
2. 各ブロックを `<section>` に割り当て、`<h2>`・`<h3>` で階層化する。
3. 列挙的な情報は `feature-list` の `<ul>/<li>` に、比較・数値データは `data-table` の `<table>` に変換する。
4. 警告・コツ・重要事項は `callout`（`--warning` / `--tip` / `--info`）で囲む。
5. すべてのクラスがBEMに準拠しているか、セマンティックタグを使っているか確認して出力する。
6. CSSを含めるよう求められた場合、または完全なページが必要な場合は reference.md の `<style>` を併せて出力する。

## チェックリスト（出力前）

- [ ] `<article>` / `<section>` / `<header>` を使用している
- [ ] すべてのクラスがBEM記法
- [ ] `<h2>` と `<h3>` で見出しが階層化されている
- [ ] `<ul>/<li>` の箇条書きがある
- [ ] `<table>`（thead/tbody）のデータ表がある
- [ ] callout の強調枠がある
