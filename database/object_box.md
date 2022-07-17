# ObjectBox

- 処理が早い（らしい）ローカルデータベース
- [Flutter で ObjectBox つかってみた](https://zenn.dev/pressedkonbu/articles/flutter-object-box)

## 概要とか準備

- 永続化のためのツール
- Entityクラスは`@Entity`と`id`というプロパティを使って自動生成を行う

```bash
# 実装に利用するpackage.
$ flutter pub add objectbox objectbox_flutter_libs

# 開発に利用するpackage.
$ flutter pub add -d build_runner objectbox_generator

# Entityの自動生成.
$ flutter pub run build_runner build
```

## 使い方の流れ

- `Store`を用意する
- `Store`から`Box`を用意する
- `Box`から`list`を取得する
- 値の追加や更新は `box.put(entity)`を利用する
- 値の削除は `box.remove(id)`を利用する