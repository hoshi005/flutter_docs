# javascript

## 変数宣言

- `var`
  - もう使わない
- `let`
  - 変数
- `const`
  - 定数

## 分割代入

- Kotlinにも登場したっぽい

```javascript
const myProfile = {
    name: '山田',
    age: 24,
};

// 分割代入
const { name, age } = myProfile;

// 順番不問
const { age, name } = myProfile;

// 別名を付与.
const { name: newName, age: newAge } = myProfile;
```

- 配列も分割代入できる

```javascript
const myProfile = ['山田', 24];

// 前から順番に変数に代入される.
const [name, age] = myProfile;

// 少ない分には問題ない
const [name] = myProfile;
```

## デフォルト値

- 関数の引数、分割代入でデフォルト値を設定可能

```javascript
const sayHello = (name = 'ゲスト') => console.log(`${name}さんこんにちは`);

sayHello();
sayHello('山田');
```

## オブジェクトの省略記法

- プロパティ名と変数名が一緒なら、省略可能

```javascript
const name = '山田';
const age = 24;

// 通常の定義.
const user = {
    name: name,
    age: age,
};

// 省略型.
const user = {
    name,
    age,
};