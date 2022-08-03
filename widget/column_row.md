# Column & Row

- https://api.flutter.dev/flutter/widgets/Column-class.html
- 
- 子要素を縦、または横に並べる。`VStack`, `HStack` のようなものか
- 子の位置調整を設定するプロパティなど

## 基本の使い方

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

## 要素のAlignmentを指定する

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

## 要素間のスペースを指定する

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

## Column, Row の全体の大きさを指定する

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

## 要素自体の大きさを指定する

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