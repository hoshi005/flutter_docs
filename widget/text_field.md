# TextField

テキスト入力を行うウィジェット。
`StatefulWidget`として利用する様子

- enabled
    - 編集可能かどうかを操作できる
- maxLength
    - 最大文字数を定義する
- maxLengthEnforcement
    - 最大文字数を超えたときの挙動を適宜できるenum
- maxLines
    - 最大行数
- decoration
    - InputDecorationを利用する
    - アイコンやプレースホルダーなどを定義する
- style
    - TextStyleを利用する
    - 入力テキストのスタイル
- controller
    - TextEditingControllerを利用する
- obscureText
    - <mark>伏せ字にする</mark>
- onChanged
    - 入力に変化があるたびに呼び出される
- onSubmitted
    - Enterキーがタップされたタイミングで呼び出される

## TextEditingController

- 入力値を取得することができる

## TextFormField

- バリデーションなどが可能

## 入力チェック手順

- `TextField`を`TextFormField`に変更する
- `TextFormField`を`Form`の子要素にする
- プロパティとして`GlobalKey<FormState>`を定義する
- `Form`の`key`にプロパティとして定義した`GlobalKey<FormState>`を指定する
- `TextFormField`の`validator`にチェックを設定する