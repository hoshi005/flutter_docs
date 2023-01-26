# TypeScript

- https://www.typescriptlang.org/
- microsoftが開発した altJS
- altJSの筆頭である
- javascriptのコードがそのまま動作する
- javascriptにデータ型の概念を持ち込んだ言語である
- コンパイルにはnode.jsが利用されるため、node.jsを入れておく必要がある
- typescriptの本体も、npmで提供されている

## TypeScriptの開発を行うために

- ちょっと試すだけであれば TypeScript Playground が便利
- 開発環境を整えるのであれば以下
  - VSCode
  - node.js
  - TypeScriptパッケージのインストール

## ユニオン型

- 複数のデータ型を | パイプ で繋いだ記述

```typescript
// string or number.
let value: string | number;

// 色々と.
let name: number | string | boolean = 123;
console.log(typeof name); // number

name = 'なまえ';
console.log(typeof name); // string

name = true;
console.log(typeof name); // boolean
```

- 型を確認する場合には、`typeof`演算子を利用する

```typescript
if (typeof name == 'string') {
  console.log('nameはstringです')
} else {
  console.log('nameはstringではありません')
}
```

## モジュール化

- 別ファイルに分けて読み込む
- 先頭に `export` をつける
  - クラス
  - 関数
  - 変数
  - インターフェイス
  - ...
- 利用する際は `import` とする

```typescript
// 一般的なimport
import { クラス名など } from "モジュールファイルのパス、拡張子なし"
// 別名を付与する
import { クラス名など as 別名 } from "モジュールファイルのパス、拡張子なし"
// 全ての定義を一括import
import * as 別名 from "モジュールファイルのパス、拡張子なし"
```

- tsファイルにおいては、`export`の記述が一つでもあれば、そのファイルはモジュールファイルとして認識される.
- `export`の記述がないファイルは、すべて同一ファイルとしてみなされる
  - `export`がないファイル`a.ts`と`b.ts`は、同じファイルとして扱われる
  - `a.ts`と`b.ts`に同じ`const num = 100`のような記述があると、重複としてエラーになる
  - なので、おまじないのように`export {}`とすることで、別ファイルとして扱う必要がある
- ファイル内にexportする定義が一つだけの場合、`default`が利用可能
  - defaultにすると、import時に`{}`が不要になる
  - これは便利なのか？？？

## 通信処理

- 最初からビルトインされている`fetch`関数をnodeで利用するなら`node-fetch`というパッケージが必要
- TypeScriptで`node-fetch`を利用する場合は、開発環境(dev dependencies)として`@types/node-fetch`パッケージが必要