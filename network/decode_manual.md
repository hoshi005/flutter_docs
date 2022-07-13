
# モデルクラスへのデコード（手動）

- このJSONをデコードするための実装

```json
{
  "kind": "youtube#channelListResponse",
  "etag": "snOQeOFzZZACQnioDea8GLleyC4",
  "pageInfo": {
    "totalResults": 1,
    "resultsPerPage": 5
  }
}
```

- 作業手順は以下の通り
    - 各種プロパティを定義する
    - コンストラクタを定義する
    - `fromJson()`を定義する
    - `toJson()`を定義する

```dart
class YoutubeModelHand {
  // 各種プロパティ.
  final String kind;
  final String etag;
  final PageInfoHand pageInfo;

  // コンストラクタ.
  YoutubeModelHand(
    this.kind,
    this.etag,
    this.pageInfo,
  );

  // fromJson().
  YoutubeModelHand.fromJson(Map<String, dynamic> json)
      : kind = json['kind'],
        etag = json['etag'],
        pageInfo = PageInfoHand.fromJson(json['pageInfo']);

  // toJson().
  Map<String, dynamic> toJson() => {
        'kind': kind,
        'etag': etag,
        'pageInfo': pageInfo,
      };
}

class PageInfoHand {
  final int totalResults;
  final int resultsPerPage;

  PageInfoHand(
    this.totalResults,
    this.resultsPerPage,
  );

  PageInfoHand.fromJson(Map<String, dynamic> json)
      : totalResults = json['totalResults'],
        resultsPerPage = json['resultsPerPage'];

  Map<String, dynamic> toJson() => {
        'totalResults': totalResults,
        'resultsPerPage': resultsPerPage,
      };
}
```

`~Repository`クラスで、レスポンスをデコードしてみる

```dart
Future<YoutubeModelHand> fetchChannels() async {
  final response = await service.fetchChannels(
    channelId: "UC5d0z8h7Pc5Evld4Dd0acMQ",
  );

  if (response.isSuccessful) {
    final model = YoutubeModelHand.fromJson(response.body);
    print(model.kind);
    print(model.etag);
    print(model.pageInfo.totalResults);
    print(model.pageInfo.resultsPerPage);
    return model;
  }
  return null;
}
```
