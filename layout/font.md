# 等幅フォントとプロポーショナルフォント

- 主にiOSで発生する問題
- フォントが等幅ではない場合（プロポーショナルフォント）
- 数値の値が変わるたびに横幅がブレる
- 解決するには以下の方法がある
  - フォントを等幅フォント（タビュラ）にする
  - `dart:ui`の`fontFeature`を指定する
    - プロポーショナルフォントであっても等幅フォントに変更可能.

```dart
import 'dart:ui';

Text(
  '123456789.......',
  style: TextStyle(
    fontSize: 64.0,
    fontFeatures: [
      FontFeature.tabularFigures(), // これを追加
    ],
  ),
),
```