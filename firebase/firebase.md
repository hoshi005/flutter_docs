# Firebase

## 組み込み

- npm で `firebase-tools` を入れる
- 以下のコマンドで `FlutterFire_cli` を入れる

```bash
$ dart pub global activate flutterfire_cli
```

- とりあえずFlutterプロジェクトに `firebase_core` を入れておく

```bash
$ flutter pub add firebase_core
```

- Firebaseのプロジェクトを作っておく
- Flutterのプロジェクト直下で以下のコマンドを実行

```bash
$ flutterfire configure
```

## firebase analytics

- Flutterプロジェクトに `firebase_analytics` を入れる

```bash
$ flutter pub add firebase_analytics
```

- `android/app/build.gradle` に以下を追加

```gradle
plugins {
    id "com.android.application"
    id "kotlin-android"
    id "dev.flutter.flutter-gradle-plugin"
    id "com.google.gms.google-services" // これを追加
}
```

- `android/build.gradle` に以下を追加

```gradle
buildscript {
    ext.kotlin_version = '1.9.10'
    repositories {
        google()
        mavenCentral()
    }

    dependencies {
        classpath 'com.android.tools.build:gradle:7.4.2'
        // START: FlutterFire Configuration
        classpath 'com.google.gms:google-services:4.3.14' // バージョンを変えた
        // END: FlutterFire Configuration
        classpath "org.jetbrains.kotlin:kotlin-gradle-plugin:$kotlin_version"
    }
}
```

- iOSもAndroidも、一旦ここまででリアルタイムに送信されることが確認できた
- AndroidはGradleへの追記や修正を忘れずに