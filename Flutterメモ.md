# Flutterメモ

<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->

<!-- code_chunk_output -->

- [Flutterメモ](#flutterメモ)
  - [基本的な記述の解説](#基本的な記述の解説)
    - [StatelessWidget](#statelesswidget)
      - [build()](#build)
    - [MaterialApp](#materialapp)
    - [Scaffold](#scaffold)
      - [appBarプロパティ](#appbarプロパティ)
      - [bodyプロパティ](#bodyプロパティ)
    - [state と setState](#state-と-setstate)
  - [Stateless と Stateful](#stateless-と-stateful)
    - [大きな違い](#大きな違い)
    - [StatefulWidget](#statefulwidget)
    - [State](#state)
  - [画面遷移](#画面遷移)
    - [push()](#push)
  - [レイアウト](#レイアウト)
    - [Container](#container)
    - [Column & Row](#column-row)
      - [基本の使い方](#基本の使い方)
      - [要素のAlignmentを指定する](#要素のalignmentを指定する)
      - [要素間のスペースを指定する](#要素間のスペースを指定する)
      - [Column, Row の全体の大きさを指定する](#column-row-の全体の大きさを指定する)
      - [要素自体の大きさを指定する](#要素自体の大きさを指定する)
    - [Text & Icon](#text-icon)
    - [MaterialApp](#materialapp-1)
  - [Text](#text)
  - [Padding, Margin](#padding-margin)
  - [Stack](#stack)
  - [Alignment](#alignment)
  - [VoidCallback](#voidcallback)
  - [GestureDetector](#gesturedetector)

<!-- /code_chunk_output -->

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


