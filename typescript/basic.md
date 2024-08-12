# Typescriptの基本

- ブラウザで動作するのはjavascriptのみ
- javascriptの癖を隠蔽するための言語がaltJS
- altJSは、javascriptにコンパイルされて動作する
- altJSの例: TypeScript, CoffeeScript, Dart
- TypeScriptは、Microsoftが開発したaltJS

# node.js

- node.jsは、本来ブラウザでしか動作しないはずのjavascriptを、サーバーサイドで動作させるための環境
- npmは、node.jsのパッケージマネージャ
- typescriptは、npmのパッケージとして提供されている

```sh
# ローカルにインストールした場合は、npxを使う
npm install typescript
npx tsc --version

# グローバルにインストールした場合は、tscコマンドが使える
npm install -g typescript
tsc --version
```