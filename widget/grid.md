# Grid

<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->

<!-- code_chunk_output -->

- [Grid](#grid)
  - [1. GridView.count](#1-gridviewcount)
  - [2. GridView.extent](#2-gridviewextent)
  - [3. GridView.builder](#3-gridviewbuilder)
    - [SliverGridDelegateWithFixedCrossAxisCount](#slivergriddelegatewithfixedcrossaxiscount)
    - [SliverGridDelegateWithMaxCrossAxisExtent](#slivergriddelegatewithmaxcrossaxisextent)
  - [横スクロール](#横スクロール)
  - [アイテムの比率](#アイテムの比率)

<!-- /code_chunk_output -->

Grid状にコンテンツを並べる場合は`GridView`を利用する。
`ListView`と同様、表示する方法はいくつかある

## 1. GridView.count

横に並べる数を固定数で指定して表示する.
あらかじめ、Widgetのリストを作成して指定する.

```dart
GridView.count(
  crossAxisCount: 2,
  padding: const EdgeInsets.all(4), // 大外のパディング
  mainAxisSpacing: 4, // アイテム間のメイン方法のパディング
  crossAxisSpacing: 4, // アイテム間のサブ方向のパディング
  children: list, // Widgetの配列.
),
```

## 2. GridView.extent

指定した数値を最大値として、それを超えない値でグリッドを並べる。
こちらも、あらかじめWidgetのリストを作成して渡す.

```dart
GridView.extent(
  maxCrossAxisExtent: 150, // 最大で幅150pとする.
  padding: const EdgeInsets.all(4),
  mainAxisSpacing: 4,
  crossAxisSpacing: 4,
  children: list,
),
```

## 3. GridView.builder

`ListView`と同様、動的に生成するための方法.
`gridDelegate`で、数を指定するのか幅を指定するのかを決められる.
`itemCount`で件数を指定しないと無限に続く.

```dart
GridView.builder(
  gridDelegate:
      // 件数指定する場合.
      SliverGridDelegateWithFixedCrossAxisCount(crossAxisCount: 2),
  itemBuilder: (BuildContext context, int index) {
    return _photoItem(list[index]);
  },
  itemCount: list.length,
),
```

### SliverGridDelegateWithFixedCrossAxisCount

`GridView.count`と同様、横に並べる件数を指定してGridを表示する.
アイテム間のスペースもここで指定する.

```dart
SliverGridDelegateWithFixedCrossAxisCount(
  crossAxisCount: 2,
  mainAxisSpacing: 4,
  crossAxisSpacing: 4
),
```

### SliverGridDelegateWithMaxCrossAxisExtent

`GridView.extent`と同様、横に並べるグリッドの最大幅を指定してGridを表示する.

```dart
SliverGridDelegateWithMaxCrossAxisExtent(
  maxCrossAxisExtent: 150,
  mainAxisSpacing: 4,
  crossAxisSpacing: 4
)
```

## 横スクロール

`ListView`と同様、横スクロールさせるには`scrollDirection`に`Axis.horizontal`を指定すれば良い.

```dart
GridView.builder(
  scrollDirection: Axis.horizontal,
  gridDelegate:
      // 件数指定する場合.
      SliverGridDelegateWithFixedCrossAxisCount(crossAxisCount: 2),
  itemBuilder: (BuildContext context, int index) {
    return _photoItem(list[index]);
  },
  itemCount: list.length,
),
```

## アイテムの比率

デフォルトは、1:1で表示される。
比率を指定する場合は`childAspectRatio`を利用する。

```dart
GridView.builder(
  scrollDirection: Axis.horizontal,
  gridDelegate: SliverGridDelegateWithFixedCrossAxisCount(
    crossAxisCount: 3,
    mainAxisSpacing: 4,
    crossAxisSpacing: 4,
    childAspectRatio: 9/16 // 比率を指定.
  ),
  itemBuilder: (BuildContext context, int index) {
    return _photoItem(items[index]);
  },
  itemCount: items.length,
  padding: const EdgeInsets.all(4),
)
```