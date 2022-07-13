# pubspec.yamlの使い方

## 依存関係の管理

- cocoapodsのような、ライブラリ管理機能
- [Flutter Packages](https://pub.dev/flutter/packages)で探す
- yaml の `dependencies` に一行追加
- `dev_dependencies` に追加されたものは、プログラム側からは利用できない
  - 開発時の環境構築などで利用する

```bash
# スペース区切りで複数追加可能.
$ flutter pub add xxxxx xxxxx xxxxx

# dev側に追加する場合は、オプションで `-d` を追加.
$ flutter pub add -d yyyyy yyyyy yyyyy
```

## 画像リソースの管理

- プロジェクト直下に`images`というディレクトリを作成
- そこに画像を配置
- `pubspec.yaml`を編集する

```yaml
# 画像を指定する
flutter:
  assets:
    - images/smaple.jpg

# ディレクトリごと指定.
flutter:
  assets:
    - images/
```

解像度ごとの指定はどうやってやるのか？？
