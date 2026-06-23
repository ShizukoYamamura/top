# Wiki Article HTML — リファレンス

`SKILL.md` のルールに基づく完全な実装リファレンス。出力時はこのテンプレートとクラス命名に従う。

## BEM クラス一覧

| Block | Element / Modifier | 用途 |
|-------|--------------------|------|
| `wiki-article` | `__header` `__title` `__lead` `__section` `__heading` `__subheading` `__text` | 記事全体 |
| `feature-list` | `__item` `__item--highlight` | 特徴の箇条書き |
| `data-table` | `__head` `__cell` `__cell--num` `__row--alt` | データ比較表 |
| `callout` | `__title` `__text` / `--info` `--tip` `--warning` `--danger` | 重要事項の強調枠 |

## 完全なHTMLテンプレート

```html
<article class="wiki-article">
  <header class="wiki-article__header">
    <h1 class="wiki-article__title">武器「サンプルライフル」攻略</h1>
    <p class="wiki-article__lead">入手方法・性能・運用のポイントをまとめたページです。</p>
  </header>

  <section class="wiki-article__section">
    <h2 class="wiki-article__heading">概要</h2>
    <p class="wiki-article__text">序盤から終盤まで使える汎用ライフル。</p>

    <h3 class="wiki-article__subheading">特徴</h3>
    <ul class="feature-list">
      <li class="feature-list__item">連射性能が高い</li>
      <li class="feature-list__item">リコイルが小さく扱いやすい</li>
      <li class="feature-list__item feature-list__item--highlight">弱点特効が高い（重要）</li>
    </ul>
  </section>

  <section class="wiki-article__section">
    <h2 class="wiki-article__heading">性能比較</h2>
    <table class="data-table">
      <thead>
        <tr>
          <th class="data-table__head">武器名</th>
          <th class="data-table__head">攻撃力</th>
          <th class="data-table__head">連射速度</th>
          <th class="data-table__head">射程</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td class="data-table__cell">サンプルライフル</td>
          <td class="data-table__cell data-table__cell--num">120</td>
          <td class="data-table__cell data-table__cell--num">85</td>
          <td class="data-table__cell data-table__cell--num">60</td>
        </tr>
        <tr class="data-table__row--alt">
          <td class="data-table__cell">比較武器A</td>
          <td class="data-table__cell data-table__cell--num">150</td>
          <td class="data-table__cell data-table__cell--num">60</td>
          <td class="data-table__cell data-table__cell--num">45</td>
        </tr>
      </tbody>
    </table>
  </section>

  <section class="wiki-article__section">
    <h2 class="wiki-article__heading">運用のコツ</h2>
    <aside class="callout callout--tip">
      <p class="callout__title">コツ</p>
      <p class="callout__text">弱点を狙うことでDPSが大きく向上します。</p>
    </aside>
    <aside class="callout callout--warning">
      <p class="callout__title">注意</p>
      <p class="callout__text">弾持ちが悪いため、予備弾薬を多めに確保すること。</p>
    </aside>
  </section>
</article>
```

## 標準スタイルシート

完全なページ出力時、またはCSSを求められた場合は `<head>` 内に以下を含める。

```html
<style>
  :root {
    --wa-bg: #ffffff;
    --wa-text: #24292f;
    --wa-muted: #57606a;
    --wa-border: #d0d7de;
    --wa-accent: #2563eb;
    --wa-info: #0969da;
    --wa-tip: #1a7f37;
    --wa-warning: #9a6700;
    --wa-danger: #cf222e;
  }

  .wiki-article {
    max-width: 820px;
    margin: 0 auto;
    padding: 1.5rem;
    color: var(--wa-text);
    background: var(--wa-bg);
    font-family: system-ui, "Segoe UI", "Hiragino Sans", "Noto Sans JP", sans-serif;
    line-height: 1.8;
  }

  .wiki-article__header {
    border-bottom: 3px solid var(--wa-accent);
    padding-bottom: 0.75rem;
    margin-bottom: 1.5rem;
  }
  .wiki-article__title { font-size: 1.9rem; margin: 0 0 0.5rem; }
  .wiki-article__lead { color: var(--wa-muted); margin: 0; }

  .wiki-article__section { margin-bottom: 2rem; }
  .wiki-article__heading {
    font-size: 1.4rem;
    border-left: 6px solid var(--wa-accent);
    padding-left: 0.6rem;
    margin: 1.5rem 0 0.75rem;
  }
  .wiki-article__subheading {
    font-size: 1.15rem;
    color: var(--wa-accent);
    margin: 1rem 0 0.5rem;
  }
  .wiki-article__text { margin: 0.5rem 0; }

  .feature-list { margin: 0.75rem 0; padding-left: 1.25rem; }
  .feature-list__item { margin: 0.35rem 0; }
  .feature-list__item--highlight { font-weight: 700; color: var(--wa-danger); }

  .data-table {
    width: 100%;
    border-collapse: collapse;
    margin: 1rem 0;
    font-size: 0.95rem;
  }
  .data-table__head {
    background: var(--wa-accent);
    color: #fff;
    text-align: left;
    padding: 0.6rem 0.75rem;
    border: 1px solid var(--wa-border);
  }
  .data-table__cell {
    padding: 0.55rem 0.75rem;
    border: 1px solid var(--wa-border);
  }
  .data-table__cell--num { text-align: right; font-variant-numeric: tabular-nums; }
  .data-table__row--alt { background: #f6f8fa; }

  .callout {
    border-left: 5px solid var(--wa-info);
    background: #f6f8fa;
    border-radius: 4px;
    padding: 0.75rem 1rem;
    margin: 1rem 0;
  }
  .callout__title { font-weight: 700; margin: 0 0 0.25rem; }
  .callout__text { margin: 0; }
  .callout--info { border-left-color: var(--wa-info); }
  .callout--tip { border-left-color: var(--wa-tip); background: #eaf6ee; }
  .callout--warning { border-left-color: var(--wa-warning); background: #fff8e6; }
  .callout--danger { border-left-color: var(--wa-danger); background: #fff0f0; }
</style>
```

## 変換例（プレーンテキスト → HTML）

**入力（ユーザーから渡されるプレーンテキスト）:**
```
回復アイテム メディキット
HPを50回復する。クールタイム30秒。
特徴: 携帯数3つまで、戦闘中でも使用可、スタックしない
比較: メディキット 回復50 重量2 / 包帯 回復20 重量1
注意: 移動しながらは使えない
```

**出力（このスキルに従ったHTML）:**
```html
<article class="wiki-article">
  <header class="wiki-article__header">
    <h1 class="wiki-article__title">メディキット</h1>
    <p class="wiki-article__lead">HPを50回復する回復アイテム。クールタイム30秒。</p>
  </header>

  <section class="wiki-article__section">
    <h2 class="wiki-article__heading">特徴</h2>
    <ul class="feature-list">
      <li class="feature-list__item">携帯数は3つまで</li>
      <li class="feature-list__item">戦闘中でも使用可能</li>
      <li class="feature-list__item">スタックしない</li>
    </ul>
  </section>

  <section class="wiki-article__section">
    <h2 class="wiki-article__heading">性能比較</h2>
    <table class="data-table">
      <thead>
        <tr>
          <th class="data-table__head">アイテム</th>
          <th class="data-table__head">回復量</th>
          <th class="data-table__head">重量</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td class="data-table__cell">メディキット</td>
          <td class="data-table__cell data-table__cell--num">50</td>
          <td class="data-table__cell data-table__cell--num">2</td>
        </tr>
        <tr class="data-table__row--alt">
          <td class="data-table__cell">包帯</td>
          <td class="data-table__cell data-table__cell--num">20</td>
          <td class="data-table__cell data-table__cell--num">1</td>
        </tr>
      </tbody>
    </table>
  </section>

  <section class="wiki-article__section">
    <h2 class="wiki-article__heading">注意点</h2>
    <aside class="callout callout--warning">
      <p class="callout__title">注意</p>
      <p class="callout__text">移動しながらは使用できない。</p>
    </aside>
  </section>
</article>
```
