# Stream

## Streamの使い方

- `sink`にデータを流すと`stream`に流れる
- `listen`で捕まえて処理する

## StreamBuilder

- 指定した`stream`にデータが流れてくると、自動で再描画が実行される
- `StatelessWidget`でも有効
- setState({})は利用しない方が良い

## BLoC

- `Business Logic Component`の略
- ビジネスロジック単位で状態管理を行うデザインパターン.
    - ビジネスロジック部分を独立させて管理し、生産性・保守性を向上させる
- 考え方としては以下の通り.
    1. インプットとアウトプットは、ストリームとシンクのみ
    1. 依存関係は注入可能で、プラットフォームに依存しない
    1. プラットフォームごとの分岐をしない
    1. 上記を守れば、どのような実装でも良い
- [こちらのイメージを参照](https://zenn.dev/kazutxt/books/flutter_practice_introduction/viewer/development_advanced4#より現実的な例)
