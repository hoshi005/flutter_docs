# 使えそうなパッケージ

## shared_preferences

- <https://pub.dev/packages/shared_preferences>

```dart
import 'package:shared_preferences/shared_preferences.dart';

saveFlag(bool flag) async {
  SharedPreferences prefs = await SharedPreferences.getInstance();
  prefs.setBool('FLAG', flag);
}
loadFlag() async {
  SharedPreferences prefs = await SharedPreferences.getInstance();
  return prefs.getBool('FLAG') ?? false;
}
```

## url_launcher

- <https://pub.dev/packages/url_launcher>
- SafariViewControllerを起動する
- Androidだとどうなるのか？

```dart
IconButton(
  icon: Icon(Icons.open_in_browser),
  onPressed: () async {
    String url = Uri.encodeFull("https://www.google.co.jp");
    if (await canLaunch(url)) {
      await launch(
        url,
        forceSafariVC: true, // アプリ内で開くことを強制.
        forceWebView: true, // アプリ内で開くことを強制.
      );
    }
  }
)
```

## flutter_launcher_icons

- <https://pub.dev/packages/flutter_launcher_icons>
- アプリアイコンを生成して配置してくれる

```yaml
dev_dependencies:
  flutter_launcher_icons: "^0.9.0"

flutter_icons:
  android: "launcher_icon"
  ios: true
  image_path: "assets/icon/icon.png"
```

上記にアイコンファイルの元を配置して以下コマンド

```bash
$ flutter pub get
$ flutter pub run flutter_launcher_icons:main
```

## font_awesome_flutter

- <https://pub.dev/packages/font_awesome_flutter>
- <https://fontawesome.com/icons?d=gallery&p=2>
- デフォルトにはない多彩なアイコン素材を利用できる

```yaml
font_awesome_flutter: ^9.0.0
```

```dart
// FaIconとIconの違いがわからない.
FaIcon(FontAwesomeIcons.amazon, color: Colors.redAccent,)
Icon(FontAwesomeIcons.amazon, color: Colors.redAccent,)
```

## flushbar / another_flushbar

- <https://pub.dev/packages/flushbar>
- <https://pub.dev/packages/another_flushbar>
- 本家が死んだ？`another`も同じ機能に見える

```dart
ElevatedButton(
  onPressed: () {
    Flushbar(
      flushbarStyle: FlushbarStyle.GROUNDED,
      backgroundColor: Colors.green,
      title: 'フラッシュバー',
      message: 'コピーしたよ',
      flushbarPosition: FlushbarPosition.TOP,
      duration: Duration(seconds: 2),
    )..show(context);
  },
  child: Text('フラッシュバー'),
),
```

![](../images/flush_bar.png)

## flutter_svg
