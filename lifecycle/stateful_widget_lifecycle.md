# `StatefulWdiget`のライフサイクル

## 画面構築

- `createState()`
    - `StatefulWidget`を構築するとすぐに呼ばれる.
    - Widgetツリーに状態を作るために呼ばれる.
- `initState()`
    - Widgetツリーの初期化を行う.
    - 一度だけ呼ばれる.
- `didChangeDependencies()`
    - `state`オブジェクトの依存関係が変更された時に呼び出される.
    - `initState`の後に呼ばれるが、それ以外にも呼ばれることはある.

## 再描画

- `build()`
    - `Widget`で作られるUIを構築する.
    - さまざまな場所から繰り返し呼び出される.
    - 変更がある部分ツリーを検知して置き換える.
- `didUpdateWidget(Widget oldWidget)`
    - ウィジェットの構成が変更されるたびに呼び出される
    - 親Widgetが変更され、再描画する必要がある場合に呼び出される.
    - `oldWidget`パラメータを取得して比較する.
- `setState()`
    - 状態が変わったことをフレームワークに通知する.

## 画面破棄

- `deactivate()`
    - `state`オブジェクトがツリーから削除するたびに呼び出される.
- `dispose()`
    - オブジェクトがツリーから完全に削除され、２度とビルドされなくなったら呼ばれる.
