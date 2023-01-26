# フロントエンド開発

- フロントエンド開発
  - ブラウザで動作するアプリケーションの開発
- altJS
  - ブラウザではjavascriptしか動作しない
  - javascriptの癖を解消するために考えだされたのがaltJS
  - altJSをコンパイルすることでjavascriptコードに変換される
    - コンパイル時にはnode.jsが使われる
- altJSの種類
  - Rubyが採用した coffeeScript
  - Googleが開発した Dart
  - Microsoftが作った Typescript
    - altJSの筆頭

## node.js

- 本来ブラウザでしか動作しないはずのjavascriptを、ブラウザなしで実行できるようにしたもの
- TypeScriptのコンパイルにも利用される
- node.js上で動作可能なjavascriptライブラリやツールはパッケージとして提供されている
- そのパッケージを管理するツールがnpm
  - node package manager
- typescriptの本体も、npmで提供されている