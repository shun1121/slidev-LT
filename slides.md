---
# try also 'default' to start simple
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://source.unsplash.com/collection/94734566/1920x1080
# apply any windi css classes to the current slide
class: 'text-center'
# https://sli.dev/custom/highlighters.html
highlighter: shiki
# show line numbers in code blocks
lineNumbers: false
# some information about the slides, markdown enabled
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
# persist drawings in exports and build
drawings:
  persist: false
# use UnoCSS (experimental)
css: unocss
---

# Newtの簡単な紹介

ブログ → https://blog-app-rouge-nine.vercel.app/ <br>
github → https://github.com/shun1121/blog-app
<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->

---

<h1 class="ml-10">Newtブログの機能と使用技術</h1>

<div class="flex mt-10">
  <div class="ml-[50px]">
    <h3>&lt;機能&gt;</h3>
    <ul>
      <li>記事一覧ページ</li>
      <li>記事詳細ページ</li>
      <li>目次のハイライト</li>
      <li>シンタックスハイライト</li>
      <li>ページネーション</li>
    </ul>
  </div>
  <div class="ml-[100px]">
    <h3>&lt;使用技術&gt;</h3>
    <ul>
      <li class="color-blue font-bold">newt-client-js</li>
      <li>Next.js（SSG）: 12.1.5</li>
      <li>React: 18.0.0</li>
      <li>TypeScript: 4.6.3</li>
      <li>Tailwind CSS: ^3.0.24</li>
      <li>ページネーション</li>
      <li>@mantine/core、hooks、next: ^4.2.6</li>
      <li>tocbot: ^4.18.2</li>
      <li>cheerio: ^1.0.0-rc.11</li>
      <li>highlight.js: ^11.5.1</li>
    </ul>
  </div>
</div>


<br>
<br>

<!--
You can have `style` tag in markdown to override the style for the current page.
Learn more: https://sli.dev/guide/syntax#embedded-styles
-->

<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 20%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

---

# Newtセットアップ

<div class="flex mb-3">
  <ol>
    <li>
      <a href="https://app.newt.so/sign-up/">https://app.newt.so/sign-up/</a>
      から会員登録。
    </li>
    <li>
      <a href="https://app.newt.so/spaces">https://app.newt.so/spaces</a>
      でスペース登録。
    </li>
    <li>
    ページ左部メニューの「Appを追加」で<br>「テンプレート」→「Blog」を選択し、追加。
    </li>
    <li>
    APIで投稿データの取得<br>
    &lt;エンドポイント&gt;<br>
    <code>https://{spaceUid}.cdn.newt.so/v1/{appUid}/{modelUid}</code><br>
    スペースUIDは、左部メニューの「スペース設定」で確認。<br>
    「Blog」テンプレートだとappUIDは「blog」、投稿データのmodelUIDは「article」。<br>
    </li>
    <li>
    最後に、メニューの「APIキー」で「Newt API Token 」を作成。
    </li>
  </ol>
  <div class="ml-10">
    <img
    class="w-auto h-30 mb-3"
    src="/signup.png"
    />
    <img
    class="w-auto h-10 mb-3"
    src="/add-app.png"
    />
    <img
    class="w-auto h-30 mb-3"
    src="/app-template.png"
    />
    <img
    class="w-auto h-30 mb-3"
    src="/setting-space.png"
    />
  </div>
</div>


<!-- --- -->
<!-- layout: image-right
image: https://source.unsplash.com/collection/94734566/1920x1080 -->
---

# データ取得
<h5>パッケージのインストール</h5>

```
yarn add newt-client-js
```
<h5>記事データ取得</h5>

```ts
import { createClient } from 'newt-client-js'

export const client = createClient({
  spaceUid: 'YOUR_SPACE_UI',
  token: process.env.API_KEY || '',
  apiType: 'api' // You can specify "cdn" or "api".
})
```
<h5>記事一覧ページで表示</h5>

```ts
export const getStaticProps: GetStaticProps<Contents<Item>> = async () => {
  const data = await client.getContents<Item>({
    appUid: 'blog',
    modelUid: 'article',
    query: { limit: 4 },
  })
  return { props: data }
}
```

---

参考

https://github.com/Newt-Inc/newt-client-js <br>
https://www.newt.so/docs/quick-start

