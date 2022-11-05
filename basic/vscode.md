# VSCodeの設定関連

<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->

<!-- code_chunk_output -->

- [VSCodeの設定関連](#vscodeの設定関連)
  - [Bundle ID と Application ID の初期設定](#bundle-id-と-application-id-の初期設定)
    - [コマンドでプロジェクトを作るなら](#コマンドでプロジェクトを作るなら)
    - [VSCodeで設定するなら](#vscodeで設定するなら)
    - [すでに作ってしまっている場合](#すでに作ってしまっている場合)
    - [参考](#参考)

<!-- /code_chunk_output -->

## Bundle ID と Application ID の初期設定

### コマンドでプロジェクトを作るなら

```bash
# --org オプションで指定する.
$ flutter create --org jp.co.shlab app001
```

### VSCodeで設定するなら

- `cmd` + `,` で設定を開く
- `organization` で検索
- `dart.flutterCreateOrganization` に `jp.co.shlab` を指定

### すでに作ってしまっている場合

- `com.example` でgrepかけて置換

### 参考

- [Flutterで作ったプロジェクトのBundleID・PckageNameを変更する方法と対策](https://www.tsuzuki817.com/posts/flutter/flutter-package-bundle/)
- [【Flutter】Bundle ID と Application ID の初期設定](https://zenn.dev/hoshi005/scraps/cc19ffbf03a2c3)