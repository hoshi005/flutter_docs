# Next.js

## プロジェクトの新規作成

```bash
# TypeScriptで作る場合
$ npx create-next-app@latest --ts next-sample

# サーバの起動.
$ npm run dev

# プロジェクトのビルド.
$ npm run build

# ビルドしたものからサーバの立ち上げ.
$ npm run start
```

- `npm run` で実行できる処理は`scripts`と呼ぶよ
- package.jsonに処理内容を書き込むよ

## Next.jsのレンダリング方法

Next.jsで利用可能なレンダリング方法には４種類ある

- 動的サイト生成
  - **SSG**: `Static Site Generation`
  - ビルド時に生成された静的コンテンツを返す
- クライアントサイドレンダリング
  - **CSR**: `Client Side Rendering`
  - 普通のReactと同じ
  - SEOには向かない
- サーバサイドレンダリング
  - **SSR**: `Server Side Rendering`
  - サーバでデータを取得し、描画してからクライアントに返す
  - SEOに効果あり
  - レスポンスが重くなる可能性あり
- インクリメンタル静的再生成
  - **ISR**: `Incremental Static Regeneration`
  - `SSG`に有効期限を設けるイメージ