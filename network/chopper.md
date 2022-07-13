# Chopperを利用したネットワーク処理

- 参考にしたのは[こちらのサイト](https://qiita.com/youmeee/items/1ee84add5b6636b96b5b)
- 作業手順はこちら
    - `pubspec.yaml`でプラグインのインストール
    - インターフェイスを定義（`~Service`）
    - 自動生成コマンドで`~Service`の実装クラスを生成
    - `ChopperClient`の生成クラスを実装（`~Creator`）
    - `~Service`クラスの通信処理を呼び出すクラスを実装（`~Repository`）
    - `~Creator`にロギング機能を実装（`interceptor`）
    - jsonのパース処理を実装する（`freezed`）

## プラグインのインストール

- 以下のプラグインをインストールする
    - [chopper](https://pub.dev/packages/chopper)
    - [build_runner](https://pub.dev/packages/build_runner)
    - [chopper_generator](https://pub.dev/packages/chopper_generator)

```yaml
dependencies:
  chopper: ^3.0.6 // 追加

dev_dependencies:
  build_runner: ^1.11.1  //追加
  chopper_generator: ^3.0.6  // 追加
```

## Serviceクラスのインターフェイスを定義

- 以下の手順で作成
    - `part`で生成後のファイル名を指定（自身のファイル名に `.chopper` を付与）
    - `@ChopperApi`でベースとなるパスを指定
    - `ChopperService`を継承した`abstruct`クラスとして定義
    - `create()`メソッドを定義

```dart
import 'package:chopper/chopper.dart';

part 'youtube_service.chopper.dart';

@ChopperApi(baseUrl: "v3")
abstract class YoutubeService extends ChopperService {
  static YoutubeService create([ChopperClient client]) =>
      _$YoutubeService(client);
}
```

- エンドポイントごとのメソッドを追加
    - `@Get`でエンドポイントを指定
    - `@Query`でクエリパラメータを指定（初期値も指定可能）
    - `@Path`でパスパラメータも指定可能

```dart
@Get(path: '/channels')
Future<Response> fetchChannels({
  @Query('part') String part,
  @Query('key') String key,
  @Query('id') String channelId,
});
```

## 自動生成コマンド

```bash
# いつものやつ
$ flutter packages pub run build_runner build --delete-conflicting-outputs
```

## ChopperClientを生成するためのクラスを実装

- 以下の手順で作成
    - `ChopperClient`を生成して返す`create()`を実装
    - この処理を`~Repository`から呼び出す想定
    - `JsonConverter()`を利用することで、レスポンスを`Map<String, dynamic>`にパースしてくれる

```dart
import 'package:chopper/chopper.dart';

class ChopperClientCreator {
  static final String baseUrl = "https://www.googleapis.com/youtube";

  static ChopperClient create() => ChopperClient(
        baseUrl: ChopperClientCreator.baseUrl,
        converter: JsonConverter(),
      );
}
```

## RepositoryクラスでAPI実行

- 以下の手順で作成
    - `ChopperClientCreator.create()`で`ChopperClient`を生成する
    - `~Service`クラスのインスタンスを生成する
    - エンドポイントごとのメソッドを用意する
    - `service`のメソッドを呼び出して実行する
    - `async`, `await` を行う

```dart
class YoutubeRepository {
  // ChopperClientを生成し、それを利用してServiceクラスを生成する.
  final YoutubeService service =
      YoutubeService.create(ChopperClientCreator.create());

  // ignore:, missing_return
  Future<Void> fetchChannels() async {
    final response = await service.fetchChannels(
      channelId: "UC5d0z8h7Pc5Evld4Dd0acMQ",
    );

    if (response.isSuccessful) {
      // developer.log(response.bodyString);
      print(response.body);
    }
  }
}
```

あとはUIから以下を行えば、通信処理が実行される

```dart
YoutubeRepository().fetchChannels();
```
