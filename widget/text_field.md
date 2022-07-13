# TextField

## 入力チェック手順

- `TextField`を`TextFormField`に変更する
- `TextFormField`を`Form`の子要素にする
- プロパティとして`GlobalKey<FormState>`を定義する
- `Form`の`key`にプロパティとして定義した`GlobalKey<FormState>`を指定する
- `TextFormField`の`validator`にチェックを設定する
