# Device Preview

- さまざまなデバイスでのレイアウト確認が簡単に行えるパッケージ.
- 言語切り替えやダークモード切り替えも簡単

## インストール

```bash
# dev ではなく 普通に組み込む.
$ flutter pub add device_preview
```
- [device_preview](https://pub.dev/packages/device_preview)

## セットアップ

- `main()`関数で`runApp()`の引数を`DevicePreview`でラップするだけ
- `wrap with builder`でやると良い
- `!kReleaseMode`を忘れずに

```dart
void main() => runApp(
  DevicePreview(
    enabled: !kReleaseMode,
    builder: (context) => MyApp(), // Wrap your app
  ),
);

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      useInheritedMediaQuery: true, // 追記.
      locale: DevicePreview.locale(context), // 追記.
      builder: DevicePreview.appBuilder, // 追記.
      theme: ThemeData.light(),
      darkTheme: ThemeData.dark(),
      home: const HomePage(),
    );
  }
}
```

- `useInherited MediaQuery` を `true` に変更
- `builder` に `DevicePreview.appBuilder` を指定
- `locale` に `DevicePreview.locale(context)` を指定