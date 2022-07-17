# debugPaintSizeEnabled

## デバッグ用の記述

- `debugPaintSizeEnabled` を `true` にすることで、レイアウトガイドを表示することができる.

```dart
// パッケージを追加
import 'package:flutter/rendering.dart';

void main() {
  debugPaintSizeEnabled = true; // 追加.
  runApp(MyApp());
}
```