# Flutter メモまとめ

<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->

<!-- code_chunk_output -->

- [Flutter メモまとめ](#flutter-メモまとめ)
  - [Flutterの勉強参考](#flutterの勉強参考)
    - [Zenn本](#zenn本)
    - [Webサイト](#webサイト)
  - [Dart基礎](#dart基礎)
    - [コンストラクタ](#コンストラクタ)
    - [factory](#factory)
    - [final](#final)
  - [Firebase関連](#firebase関連)
    - [導入](#導入)
    - [Firebase Auth](#firebase-auth)
    - [Firestoreの操作](#firestoreの操作)
      - [モデルクラス](#モデルクラス)
      - [withConverter](#withconverter)
      - [データの追加](#データの追加)
      - [データの取得](#データの取得)
      - [データの取得（リアルタイム）](#データの取得リアルタイム)
  - [さまざまなUI](#さまざまなui)
    - [NavigationRail サイドナビ](#navigationrail-サイドナビ)
    - [Expanded　と Flexible](#expanded-と-flexible)
    - [ClipPath で描画](#clippath-で描画)
    - [CustomPaint で描画](#custompaint-で描画)

<!-- /code_chunk_output -->

## Flutterの勉強参考

### Zenn本

- [作って学ぶ、FlutterとFirebaseを使ったアプリ開発](https://zenn.dev/umatoma/books/1f4cb2404f3fa9)
  - FirebaseでAuthenticationやfirestoreなどを扱う
- [入門 Riverpod](https://zenn.dev/umatoma/books/bd010486772aff)
  - Riverpodをさらっと一通り扱う
- [Flutter x Riverpod でアプリ開発！実践入門](https://zenn.dev/riscait/books/flutter-riverpod-practical-introduction)
  - Riverpodについて細かく解説
  - 更新も早いので、Riverpodについてはこれで十分な気がする
- [Flutterの教科書 by Flutter大学](https://zenn.dev/flutteruniv/books/flutter-textbook)
  - Flutter大学なので、初学者に優しい
  - Widgetの解説などが丁寧

### Webサイト

- [flutter-study.dev](https://www.flutter-study.dev)
  - 少し古いが、firebaseやproviderなどを一通りさらっと
  - Firebaseを使ったリアルタイムチャットは秀逸だったかも
- [【Flutter】dioを使ってAPI通信をする！サンプルを用いて解説](https://terupro.net/flutter-api-dio-sample)
  - <mark>通信周りとriverpodの使い方</mark>
  - 他の記事も結構参考になりそう

---

## Dart基礎

### コンストラクタ

- `{...}`をつけると、名前付き引数になる

```dart
class PixabayImage {
  final String webformatURL;
  final String previewURL;
  final int likes;

  PixabayImage({
    required this.webformatURL,
    required this.previewURL,
    required this.likes,
  });
}
```

### factory

- `factory`で、独自のファクトリーメソッドが作成可能

```dart
factory PixabayImage.fromMap(Map<String, dynamic> map) {
  return PixabayImage(
    webformatURL: map['webformatURL'],
    previewURL: map['previewURL'],
    likes: map['likes'],
  );
}
```

### final

- `final`をつけて初期値を与えれば、型を省略できる

---

## Firebase関連

### 導入

- FlutterアプリにFirebaseを導入する方法はZennにまとめてある
  - [FlutterにFirebaseを組み込む](https://zenn.dev/hoshi005/scraps/7397d635049fac)

### Firebase Auth

- ID, Pass なら `firebase_auth` のみでOK
- Google Signin でログインするなら `google_sign_in` も使う
  - [参考 Flutter大学](https://zenn.dev/flutteruniv/books/flutter-textbook/viewer/make-chat#googlesignin-を実装しよう)
- Android はフィンガープリントを用意
- <mark>iOS は Info.plist にスキームの戻り設定を追加する？？？</mark>
  - それだけだと、キャンセル時にクラッシュする様子

### Firestoreの操作

#### モデルクラス

- snapshot ←→ モデルクラス
- 変換のための関数を用意しておくと良い

#### withConverter

- `withConverter`を使って`CollectionReference`を作成しておくと便利.

```dart
final postsReference =
    FirebaseFirestore.instance.collection('posts').withConverter(
  fromFirestore: (snapshot, _) {
    return Post.fromFirestore(snapshot);
  },
  toFirestore: (value, _) {
    return value.toMap();
  },
);
```

#### データの追加

- `add()`の代わりに`docs().set()`でもOK
- 参考
  - [Firestoreでデータ保存](https://www.flutter-study.dev/firebase-app/firestore)

```dart
await FirebaseFirestore.instance
    .collection('posts')
    .add({
      'text': ........,
      'email': .......,
      'date': ........,
    });
```

#### データの取得

- `FutureBuilder`と`QuerySnapshot`を利用する
- 参考
  - [Firestoreでデータ保存](https://www.flutter-study.dev/firebase-app/firestore)

```dart
FutureBuilder<QuerySnapshot>(
    future: FirebaseFirestore.instance
        .collection('posts')
        .orderBy('date')
        .get(),
    builder: (context, snapshot) {
      if (snapshot.hasData) {
        final List<DocumentSnapshot> documents = snapshot.data!.docs;
        // 以下省略.
      }
    },
)
```

#### データの取得（リアルタイム）

- `FutureBuilder`の代わりに`StreamBuilder`を利用する
- `get()`の代わりに`snapshot()`を利用する
- それ以外は同じ
- 参考
  - [Firestoreでリアルタイム更新](https://www.flutter-study.dev/firebase-app/firestore-stream)

---

## さまざまなUI

### NavigationRail サイドナビ

- [NavigationRail class](https://api.flutter.dev/flutter/material/NavigationRail-class.html)
- 画面左側にアイコンを並べるようなナビゲーション

### Expanded　と Flexible

- `Row` と `Column` の中で利用する
- 子要素を引き伸ばす、もしくは縮める
- 違いはこちら
  - [Flexible と Expanded って何が違うんだっけ？](https://zenn.dev/pressedkonbu/articles/flexible-vs-expanded)

### ClipPath で描画

- `Container`を`ClipPath`でくり抜く
- [Youtubeで概要説明](https://www.youtube.com/watch?v=oAUebVIb-7s)

### CustomPaint で描画

- pathなどで描画する
- [Youtubeで概要説明](https://www.youtube.com/watch?v=kp14Y4uHpHs)
