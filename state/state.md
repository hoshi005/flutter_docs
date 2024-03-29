# 状態管理

## 状態管理で考えるべきこと

おおきく２つある

- データを保存する場所
- データの流れの方向性

## データを保存する場所

- グローバル環境への保存
  - 手軽な管理
  - singleton
  - スケールしない
    - 同じような情報はコピペし、肥大化・冗長化してしまう
  - 誰でも参照・変更可能
  - 単体テストが大変
- flutterの多くの手法は**グローバルではない**
  - Provider
  - InheritedWidget
  - ツリー状の子孫に対してのみ伝える

## データの流れの方向性

- 現代の開発では**一方通行であることが重要**
  - 変更側と参照側に分けた場合、参照者からは変更できないこと
  - 不具合があっても、変更側か参照側か、原因の特定が容易
- StatefulWidgetのsetState
  - どこからでも変更可能
  - **一方通行ではない**
- Redux
  - グローバル環境を利用している
  - **一方通行である**