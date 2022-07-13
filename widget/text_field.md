# TextField

テキスト入力を行うウィジェット。
`StatefulWidget`として利用する様子

- autofocus
  - 自動的にフォーカスさせる
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

- `TextFormField`に設定することで、任意のタイミングで値の操作などができる
- 入力値を取得する
- 入力値をクリアする

## TextFormField

- バリデーションなどが可能

## 入力チェック手順

- `TextField`を`TextFormField`に変更する
- `TextFormField`を`Form`の子要素にする
- プロパティとして`GlobalKey<FormState>`を定義する
- `Form`の`key`にプロパティとして定義した`GlobalKey<FormState>`を指定する
- `TextFormField`の`validator`にチェックを設定する

## キーボードを閉じる

- `FocusScope`の`unfocus()`を呼び出すことでキーボードを閉じることが可能
- `Scaffold`ごと`GestureDetector`でラップし、`onTap()`で以下を呼び出すなど.

```dart
FocusScope.of(context).unfocus();
```

