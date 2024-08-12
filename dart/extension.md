# 拡張

## implement

全てのクラスは暗黙的なインターフェイスを持っている

```dart
class Animal {
    void bark() {
        print('bark');
    }
}

/// implementsした場合は、オーバーライドが必須
class Dog implements Animal {
    @override
    void bark() {
        print('wanwan');
    }
}

/// extendsした場合は、オーバーライドが任意
class Cat extends Animal {
}
```

## extension

拡張名を省略した場合は、同一ファイルからのみ利用可能.

```dart
// 拡張名を省略
extension on List<T> {
    ...
}
```