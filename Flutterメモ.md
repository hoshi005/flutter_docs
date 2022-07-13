# Flutterメモ

## 基本的な記述の解説

### StatelessWidget

- `StatelessWidget`を継承することでアプリ自体が`Widget`になる
- Flutterでは、配置やパディング、レイアウトに関するほとんど全てが`Widget`でできている
- そのほかの`Widget`に関しては[公式のドキュメント](https://flutter.dev/docs/development/ui/widgets)を確認するとよい
- `StatefulWidget`というものもあるよう

#### build()

- Widgetが持つメソッド
- このメソッドの中でUIを作成する
- SwiftUIでいうところの `var body: some View` みたいなもの
- 必要に応じて呼び出され、画面が再構築される

### MaterialApp

- マテリアルデザインのアプリを作成するためのWidget
- まずは最初にこいつを`return`すればよさそう
- `title`に指定した文字列は、Androidのタスクスイッチャー状態で表示される。iOSでは意味がないらしい。**とりあえずアプリのタイトルをつけておけばよさそう**。

### Scaffold

- `AppBar`やタイトル、ホーム画面のウィジェットツリーを保持する`body`プロパティを提供
- ウィジェットのサブツリーは大きくなりがち
- `appBar`プロパティ
- `body`プロパティ

#### appBarプロパティ

- `appBar`にはWidgetのヘッダに表示する`AppBar`を表現することができる
- [AppBarの公式のドキュメント](https://api.flutter.dev/flutter/material/AppBar-class.html)はこちら

#### bodyプロパティ

- `body`にはさまざまなレイアウトを指定可能
- [レイアウトの公式ドキュメント](https://flutter.dev/docs/development/ui/layout)はこちら

### state と setState

- `setState()`を呼び出すと、Flutterフレームワークに`State`の変化を伝え、`build()`が再構築される

## Stateless と Stateful

### 大きな違い

- `Stateless`は普遍
  - プロパティを変更することができない
- `Stateful`は変更がある
  - `StatefulWidget`クラスをつくる
  - `State`クラスを作る（状態保持クラス）

### StatefulWidget

- `createState()`で`State`クラスを返すだけ？

### State

- StatefulWidgetをジェネリクスにした`State`を継承する
- `build()`を実装して実際にUIを構築するのはこっち
- `setState()`の中でプロパティに変更を加えると、`build()`が再構築される？

## 画面遷移

`Navigator`を利用することで画面遷移が行える.

- `Navigator.of(context).push()`
- `Navigator.of(context).pop()`

### push()

- `MaterialPageRoute()`

## レイアウト

### デバッグ用の記述

`debugPaintSizeEnabled`を`true`にすることで、レイアウトガイドを表示することができる.

```dart
// パッケージを追加
import 'package:flutter/rendering.dart';

void main() {
  debugPaintSizeEnabled = true; // 追加.
  runApp(MyApp());
}
```

### Container

内包する子ウィジェットをカスタマイズするために利用する

- padding
- margin
- border
- 背景色
- など

```dart
child: Container(
  color: Colors.blue,
  width: 300,
  height: 300,
  child: Text('word', style: TextStyle(color: Colors.white,),),
  margin: const EdgeInsets.all(100),
  alignment: Alignment.center.
  transform: Matrix4.rotationZ(0.1)
),
```

### Column & Row

子要素を縦、または横に並べる。`VStack`, `HStack` のようなものか

- 子の位置調整を設定するプロパティなど

#### 基本の使い方

```dart
child: Row(
  children: [
    Container(width: 100, height: 100, color: Colors.blue,),
    Container(width: 100, height: 100, color: Colors.yellow,),
  ]
),

child: Column(
  children: [
    Container(width: 100, height: 100, color: Colors.blue,),
    Container(width: 100, height: 100, color: Colors.yellow,),
  ]
),
```

#### 要素のAlignmentを指定する

要素の位置調整を行う場合は、`MainAxisAlignment`, `CrossAxisAlignment`を利用する

```dart
child: Row(
  mainAxisAlignment: MainAxisAlignment.end,
  crossAxisAlignment: CrossAxisAlignment.start,
  children: [
    Container(width: 100, height: 100, color: Colors.blue,),
    Container(width: 100, height: 100, color: Colors.yellow,),
  ]
),
```

#### 要素間のスペースを指定する

要素間のスペースを調整する場合は以下のようにする

```dart
child: Row(
  mainAxisAlignment: MainAxisAlignment.spaceAround,
  children: [
    Container(width: 100, height: 100, color: Colors.blue,),
    Container(width: 100, height: 100, color: Colors.yellow,),
  ]
),
```

- `spaceAround`: 開始位置と終了位置を**適切に取る**
- `spaceBetween`: 開始位置と終了位置を**なしにする**
- `spaceEvenly`: 開始位置と終了位置を**要素同士の間隔と同じだけ取る**

#### Column, Row の全体の大きさを指定する

要素全体の大きさを指定する場合は`MainAxisSize`を利用する

```dart
child: Row(
  mainAxisSize: MainAxisSize.max,
  mainAxisAlignment: MainAxisAlignment.center,
  children: <Widget>[
    Container( color: Colors.blue, width: 50, height:50 ),
    Container( color: Colors.red, width: 50, height:50 ),
    Container( color: Colors.green, width: 50, height:50 ),
    Container( color: Colors.orange, width: 50, height:50 ),
  ],
),
```

- `max`: 要素いっぱいまで広げる
- `min`: 要素が必要な部分までしか使わない

#### 要素自体の大きさを指定する

`Expand`を利用することで、要素自体の大きさを最大まで指定することができる

```dart
child: Column(
  children: [
    Expanded(
      child: Container(color: Colors.blue,),
    ),
    Expanded(
      flex: 2,
      child: Container(color: Colors.yellow,),
    ),
    Expanded(
      child: Container(color: Colors.pink,),
    ),
  ],
),
```

### Text & Icon

- Iconの色は`color`プロパティ
- Textのフォント・色・太さなどの見た目は`style`プロパティ

### MaterialApp

これを指定すると、Googleが推奨するデザインになる

- フォントサイズ
- フォントカラー
- などなど？？？

## Text

```dart
new Text(
  'Welcome to Flutter Tutorial.',
  style: TextStyle(
    color: Colors.blue,
    fontSize: 25,
  ),
)
```

## Padding, Margin

```dart
const EdgeInsets.all(50)
const EdgeInsets.only(left: 50)
```

## Stack

- `Widget`を重ねて配置することができるWidget
- [こちらの記事](https://dev.classmethod.jp/articles/flutter_stack1/)が非常に参考になった

```dart
Stack(
  children: [
    Container(
      width: 100,
      height: 100,
      color: Colors.blue,
    ),
    Container(
      width: 50,
      height: 50,
      color: Colors.yellow,
    ),
  ]
),
```

Stackの子要素としては`positioned`と`non-positioned`の２種類がある。`positioned`な要素とは、`Positioned`ウィジェットでラップされたものを指す。それ以外は`non-positioned`となる。

- positioned
    - `Positioned`ウィジェットでラップされたWidget
- non-positioned
    - 普通のウィジェット

```dart
// positionedなウィジェット.
Stack(
  children: <Widget>[
    Positioned(
      left: 20.0,
      top: 20.0,
      width: 100.0, // サイズを指定している
      height: 100.0,
      child: Container(color: Colors.indigo,),
    ),
    Positioned(
      left: 100.0,
      top: 100.0,
      right: 100.0, // 上下左右の位置を指定している.
      bottom: 200.0,
      child: Container(color: Colors.cyan,),
    ),
  ],
);
```

`alignment`を指定した場合。ちょっと混乱するかも。

```dart
Stack(
  alignment: Alignment.bottomRight,
  children: <Widget>[
    SizedBox(
      width: 200.0,
      height: 200.0,
      child: Container(color: Colors.orange,),
    ),
    SizedBox(
      width: 100.0,
      height: 100.0,
      child: Container(color: Colors.cyan,),
    ),
    Text("Test"),
    Positioned(
      top: 20.0,
      left: 20.0,
      right: 70.0,
      bottom: 70.0,
      child: Container(color:Colors.green),
    )
  ]
);
```

- `Stack`は全ての`non-positioned`を描画して**それを包括できるサイズになる**
- ただし、`non-positioned`が1つも存在しない時は、**可能な限り大きくなる**

## Alignment

```dart
Alignment.topLeft
Alignment.centerRight
```

`Alignment`クラスには他にも以下のようなものがあります。

| left | center | right |
| --- | --- | --- |
| topLeft | topCenter | topRight |
| centerLeft | center | centerRight |
| bottomLeft | bottomCenter | bottomRight |

## List

一覧を表示する際は `ListView` を利用する。
表示する要素やデータによって、コンストラクタを切り替えて利用する。

### 1. デフォルトコンストラクタ

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

### 2. ListView.builder

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

### 横スクロール

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

## Grid

Grid状にコンテンツを並べる場合は`GridView`を利用する。
`ListView`と同様、表示する方法はいくつかある

### 1. GridView.count

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

### 2. GridView.extent

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

### 3. GridView.builder

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

#### SliverGridDelegateWithFixedCrossAxisCount

`GridView.count`と同様、横に並べる件数を指定してGridを表示する.
アイテム間のスペースもここで指定する.

```dart
SliverGridDelegateWithFixedCrossAxisCount(
  crossAxisCount: 2,
  mainAxisSpacing: 4,
  crossAxisSpacing: 4
),
```

#### SliverGridDelegateWithMaxCrossAxisExtent

`GridView.extent`と同様、横に並べるグリッドの最大幅を指定してGridを表示する.

```dart
SliverGridDelegateWithMaxCrossAxisExtent(
  maxCrossAxisExtent: 150,
  mainAxisSpacing: 4,
  crossAxisSpacing: 4
)
```

### 横スクロール

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

### アイテムの比率

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

## VoidCallback

コールバックを引数に指定する際に利用する。
`VoidCallback`は、引数なし・戻り値なし

```dart
// コールバックを受け取るメソッドを定義.
Widget _function(VoidCallback callback) {
  return RaisedButton(
    child: Text("コールバックボタン."),
    onPressed: callback
  );
}

// 普通の書き方.
_function(() {
  print("ボタンがタップされました");
});

// 省略形の書き方.
_function(() => print("ボタンがタップ."));
```

## GestureDetector

タップアクションに反応させるためのウィジェット.



## TextField

テキスト入力を行うウィジェット。
`StatefulWidget`として利用する様子

- enabled
    - 編集可能かどうかを操作できる
- maxLength
    - 最大文字数を定義する
- maxLengthEnforcement
    - 最大文字数を超えたときの挙動を適宜できるenum
- maxLines
    - 最大行数
- decoration
    - InputDecorationを利用する
    - アイコンやプレースホルダーなどを定義する
- style
    - TextStyleを利用する
    - 入力テキストのスタイル
- controller
    - TextEditingControllerを利用する
- obscureText
    - 伏せ字にする
- onChanged
    - 入力に変化があるたびに呼び出される
- onSubmitted
    - Enterキーがタップされたタイミングで呼び出される

### TextEditingController

- 入力値を取得することができる

### TextFormField

- バリデーションなどが可能
