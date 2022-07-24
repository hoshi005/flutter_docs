# Container

- https://api.flutter.dev/flutter/widgets/Container-class.html
- childがいない場合、最大に広がる
- childがいる場合、childのサイズになる

## 概要とか

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

## margin と padding

- margin は、ウィジェットの外側のスペース
- padding は、ウィジェットの内側のスペース