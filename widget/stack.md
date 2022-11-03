# Stack

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