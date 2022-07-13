# モデルクラスへのデコード（自動）

- 上記のように`fromJson()`, `toJson()` を記述するのがしんどい
- ある程度の記述を自動化する
- 作業手順は以下のとおり
    - プラグインのインストールを行う
    - モデルクラスを定義する
    - 自動生成コマンド

## プラグインのインストール

- 以下のプラグインをインストールする
    - [json_annotation](https://pub.dev/packages/json_annotation)
    - [json_serializable](https://pub.dev/packages/json_serializable)

```yaml
dependencies:
  json_annotation: ^3.1.1

dev_dependencies:
  json_serializable: ^3.5.1
```

## モデルクラスの定義

- 作業手順は以下の通り
    - `part`で生成後のファイル名を指定（自身のファイル名に `.g` を付与）
    - クラス定義に`@JsonSerializable()`を定義
        - 入れ子の場合は、親側に`explicitToJson: true`を指定
    - 各種プロパティとコンストラクタを定義
    - `fromJson()`, `toJson()` を定められたフォーマットで定義

```dart
import 'package:json_annotation/json_annotation.dart';

part 'youtube_model_auto.g.dart';

@JsonSerializable(explicitToJson: true)
class YoutubeModelAuto {
  final String kind;
  final String etag;
  final PageInfoAuto pageInfo;

  YoutubeModelAuto(
    this.kind,
    this.etag,
    this.pageInfo,
  );

  factory YoutubeModelAuto.fromJson(Map<String, dynamic> json) =>
      _$YoutubeModelAutoFromJson(json);

  Map<String, dynamic> toJson() => _$YoutubeModelAutoToJson(this);
}

@JsonSerializable()
class PageInfoAuto {
  final int totalResults;
  final int resultsPerPage;

  PageInfoAuto(
    this.totalResults,
    this.resultsPerPage,
  );

  factory PageInfoAuto.fromJson(Map<String, dynamic> json) =>
      _$PageInfoAutoFromJson(json);

  Map<String, dynamic> toJson() => _$PageInfoAutoToJson(this);
}
```

## 自動生成コマンド

```bash
# いつものやつ
$ flutter packages pub run build_runner build --delete-conflicting-outputs
```

## 使ってみる

- 使い方は手動と同じ
- **fromJson(), toJson() の記述量が減って楽になる！**
