# FVM

- バージョン管理用のツール

## インストール

- homebrew でインストール

```bash
$ brew tap leoafarias/fvm
$ brew install fvm
```

## 使い方

- flutterのプロジェクトルートで `use` コマンド

```bash
$ fvm use 3.0.5
```

- プロジェクトですでに `.fvm/fvm_config.json` が存在する場合は、すでにバージョンが決まっている
- その場合は、そのバージョンに合わせてflutterをインストールする

```bash
$ fvm install
```

## VSCodeの設定

- setting.json 開く
- 以下を追加

```json
{
  "dart.flutterSdkPath": ".fvm/flutter_sdk"
}
```