# アプリのライフサイクル

- `State` に `WidgetsBindingObserver` を実装
- 自身をObserverとして登録

```dart
@override
void initState() {
  super.initState();
  WidgetsBinding.instance!.addObserver(this);
}

@override
void dispose() {
  WidgetsBinding.instance!.removeObserver(this);
  super.dispose();
}

@override
void didChangeAppLifecycleState(AppLifecycleState state) {
  print('state = $state');
  switch (state) {
    case AppLifecycleState.inactive:
      print('非アクティブになった');
      break;
    case AppLifecycleState.paused:
      print('停止された');
      break;
    case AppLifecycleState.resumed:
      print('再開された');
      break;
    case AppLifecycleState.detached:
      print('破棄された');
      break;
  }
}
```

非アクティブが複数回呼び出されているように見える。
