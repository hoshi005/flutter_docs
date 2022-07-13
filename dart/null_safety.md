# NullSafety

## Null-aware演算子

`2.12`以前でも利用可能な、nullをある程度回避可能な演算子.

### `?.`演算子

オブジェクトの`null`をチェックしてからアクセスする.

```dart
x = nullableInstance?.method();

// 等価な処理.
if (nullableInstance != null) {
  x = nullableInstance.method();
}
```

### `??`演算子

代入する変数が`null`でないならその値を利用し、`null`なら右辺を利用する.

```dart
x = nullable ?? 0;

// 等価な処理.
x = (nullable != null) ? nullable : 0;
```

### `??=`演算子

変数が`null`でないならば値を変えず、`null`なら右辺を利用する.  
値がない場合の初期化などに利用する.

```dart
x ??= 0;

// 等価な処理.
x = x ?? 0;
```

## NullSafety

宣言時に、null許容型かどうかを明言する.

```dart
int? a
int b
```
