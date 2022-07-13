# インストール

- 任意のディレクトリにSDKを配置
  - とりあえずホームディレクトリに
- パスを通す
```bash
# flutter の設定.
$ export PATH="$PATH:$HOME/flutter/bin"
```
- Flutter Tool を事前にダウンロード
```bash
$ flutter precache
```
- 開発に必要なソフトウェアがインストールされているか確認
```bash
$ flutter doctor
```
- 適当にプロジェクトを作成
```bash
$ flutter create my_app
```
- 実行してみる
```bash
$ flutter run
```
- 終了する時は`q`を押下
- 開発環境として利用可能なのは以下の３つ（とりあえず Android Studio を利用）
  - Android Studio
  - IntelliJ IDEA
  - Visual Studio Code
- 事前にエミュレータを作成しておく
- Flutterプラグインをインストール
  - Preferences → Plugins から選択
  - Flutterプロジェクトを作成可能になる
- iOSについては、一度Xcodeで開いて team の設定を行えばビルド可能
