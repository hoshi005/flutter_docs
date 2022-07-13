# Dart

## ログ出力

- `print(xxx)`でいける
- 出力情報量に上限があるようなので、`developer.log(xxx)`を利用する

```dart
import 'dart:developer' as developer;

// 文字列以外なら toString() が必要かも.
developer.log('AAA AAA');
```

## アンダーバー (\_)

- Dart では`private`を意味する
- クラス内からしかアクセスできなくなる
- 変数やメソッドに利用可能

## ゼロパディング

動き的にも早いらしい.

```dart
print(1.toString().padLeft(3, "0")); // => 001
print("ABC".padLeft(5, "x")); // => xxABC
```

## 配列操作

### 数値から生成する

```dart
var list = new List.generate(10, (i) => i);
// [0, 1, 2, 3, 4, 5, ... 9]
```

### forEach()

```dart
fruits.forEach((fruit) => print(fruit));
// banana apple orange
```

### map()

```dart
var mappedFruits = fruits.map((fruit) => "I love $fruit !").toList();
// I love banana ! I love apple ! I love orange !
```

### contains()

```dart
print(numbers.contains(6)); // => false.
print(fruits.contains("apple")); // => true.
```
