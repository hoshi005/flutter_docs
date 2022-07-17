# モデルクラスへのデコード（freezed）

- `json_serializable`を利用してもそれなりに記述量があるのでもっと減らす
- `freezed`を利用すれば、`toJson()`なども自動生成される
- 作業手順は以下のとおり（通常の自動生成と同じ）
    - プラグインのインストールを行う
    - モデルクラスを定義する
    - 自動生成コマンド

## プラグインのインストール

- 以下のプラグインをインストールする
    - [freezed_annotation](https://pub.dev/packages/freezed_annotation)
    - [freezed](https://pub.dev/packages/freezed)

```yaml
dependencies:
  freezed_annotation: ^0.12.0

dev_dependencies:
  freezed: ^0.12.7
```

## モデルクラスの定義

- 作業手順は以下の通り
    - `part`で生成後のファイル名を指定（自身のファイル名に `.freezed`, `.g` を付与）
    - クラス定義に`@freezed`を定義
    - `with`で、定められたフォーマットのクラスをmix-in
    - コンストラクタを定められたフォーマットで定義
    - `fromJson()` を定められたフォーマットで定義
- コンストラクタを作った時点で一度自動生成コマンドをやってしまった方が楽かも？？

```dart
import 'package:freezed_annotation/freezed_annotation.dart';

part 'youtube_model_freezed.freezed.dart';
part 'youtube_model_freezed.g.dart';

@freezed
abstract class YoutubeModelFreezed with _$YoutubeModelFreezed {
  const factory YoutubeModelFreezed({
    String kind,
    String etag,
    PageInfoFreezed pageInfo,
  }) = _YoutubeModelFreezed;

  factory YoutubeModelFreezed.fromJson(Map<String, dynamic> json) =>
      _$YoutubeModelFreezedFromJson(json);
}

@freezed
abstract class PageInfoFreezed with _$PageInfoFreezed {
  const factory PageInfoFreezed({
    int totalResults,
    int resultsPerPage,
  }) = _PageInfoFreezed;

  factory PageInfoFreezed.fromJson(Map<String, dynamic> json) =>
      _$PageInfoFreezedFromJson(json);
}
```

## 自動生成コマンド

```bash
# いつものやつ
$ flutter packages pub run build_runner build --delete-conflicting-outputs
```

## 使ってみる

- 使い方は手動と同じ
- **さらに記述量が減って楽になる！**
- **書き方にクセがある！！**

## 参考

- スニペットを使って記述を省略
  - [Flutter開発を加速するVSCodeスニペットの使い方](https://zenn.dev/k9i/articles/70798511bac2b9)
  - VSCodeにもプラグインらしきものがあるらしい？
- JSONのキー名と変数名が違う場合は`@JsonSerializable`を利用する
  - [【Flutter】freezedで大文字のField名のJSONをパースする方法](https://note.com/minato_i/n/n6fc0410d96e3)
