# List

<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->

<!-- code_chunk_output -->

- [List](#list)
  - [1. デフォルトコンストラクタ](#1-デフォルトコンストラクタ)
  - [2. ListView.builder](#2-listviewbuilder)
  - [横スクロール](#横スクロール)

<!-- /code_chunk_output -->

一覧を表示する際は `ListView` を利用する。
表示する要素やデータによって、コンストラクタを切り替えて利用する。

## 1. デフォルトコンストラクタ

`ListView()`を利用する方法。静的なリスト。`children`のみ指定可能。`builder`がないので、**事前にウィジェットの一覧を作成**しておく必要がある。

```dart
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    const data = [
      Text("item0"),Text("item1"),Text("item2"),Text("item3"),Text("item4"),
    ];
    return MaterialApp(
      home: Scaffold(
        body: ListView(
          children: data
        ),
      ),
    );
  }
}
```

`ListTile`を利用すると、セル一つ一つを一般的な見せ方で作成できる。

## 2. ListView.builder

主に動的なリストを作成する際に利用する。`ListView.builder()`の引数`itemCount`を指定すれば、リスト数を制限できる。

```dart
class List02 extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    var list = ["ロコ", "四条貴音", "高坂海美", "最上静香", "田中琴葉", "白石紬",];

    return MaterialApp(
      title: "List 02",
      home: Scaffold(
        appBar: AppBar(
          title: Text("ListView"),
        ),
        body: ListView.builder(
          itemBuilder: (BuildContext context, int index) {
            return _messageItem(list[index]);
          },
          itemCount: list.length, // 件数をここで指定する.
        ),
      ),
    );
  }
}
```

## 横スクロール

ListViewを横スクロールさせるには、`scrollDirection`を指定する.

```dart
ListView.builder(
  scrollDirection: Axis.horizontal,
  itemBuilder: (BuildContext context, int index) {
    // TODO:
  },
  itemCount: 5
),
```