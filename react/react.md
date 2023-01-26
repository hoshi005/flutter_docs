# React

<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->

<!-- code_chunk_output -->

- [React](#-react)
  - [コンポーネント](#-コンポーネント)
    - [クラスコンポーネント.](#-クラスコンポーネント)
    - [関数コンポーネント.](#-関数コンポーネント)
    - [なぜコンポーネントを使うのか](#-なぜコンポーネントを使うのか)
    - [コンポーネントの基本的な使い方](#-コンポーネントの基本的な使い方)
    - [propsでデータを受け渡す](#-propsでデータを受け渡す)
  - [Hooksとは](#-hooksとは)
    - [なぜstateを使うのか？](#-なぜstateを使うのか)
    - [useStateによるstateの宣言方法](#-usestateによるstateの宣言方法)
    - [propsとstateの違い](#-propsとstateの違い)
  - [ライフサイクルとは](#-ライフサイクルとは)
    - [3種類のライフサイクル](#-3種類のライフサイクル)
    - [useEffect](#-useeffect)
    - [useEffectの実行タイミング](#-useeffectの実行タイミング)
    - [クリーンナップ関数](#-クリーンナップ関数)
    - [useEffectのユースケース](#-useeffectのユースケース)

<!-- /code_chunk_output -->

## コンポーネント

- **見た目**と**機能**を合わせ持つUI部品
- コンポーネントを組み合わせてページを作る
- コンポーネントは２つある
  - クラスコンポーネント
  - 関数コンポーネント（Functional Component）
- クラスコンポーネントは使われない

### クラスコンポーネント.

```javascript
class Button extends Component {
  render() {
    // 中身はJSX
    return <button>Say, {this.props.hello}</button>
  }
}
export default Button;
```

### 関数コンポーネント.

- 2020年2月にでたReact`16.7`
- React Hooksの登場で、Classと同じことができるようになった
  - stateを扱えるようになった
  - ライフサイクルを扱えるようになった
- であれば記述量が少ない関数コンポーネントでいいじゃない.

```javascript
const Button = (props) => {
  // 中身はJSX
  return <button>Say, {props.hello}</button>
}
export default Button;
```

### なぜコンポーネントを使うのか

- 再利用するため
  - 記述量が減る
- コードの見通しをよくするため
  - １ファイル、１コンポーネント
  - 別ファイルに分けると、コードが見やすくなる
- 変更に強くするため
  - 修正は１回署だけでOK

### コンポーネントの基本的な使い方

- 子コンポーネントは呼ばれる
- 親コンポーネントは子を呼ぶ

### propsでデータを受け渡す

- propsのデータは{}で渡す
- 文字列はそのままでもOK
- 文字列、数値、真偽値、配列、オプジェクト、日付もOK
- 変数を渡すのもあり

## Hooksとは

- Hooks = クラスコンポーネントの機能に接続するもの
- クラスコンポーネントでしか使えなかった機能が、関数コンポーネントでも使えるようになった
  - 状態管理
  - ライフサイクル

### なぜstateを使うのか？

- Reactコンポーネント内の値を書き換えたい
  - DOMで直接書き換えるのは❌
  - 新しい値を使って再描画（再レンダリング）させる
- Reactコンポーネントが再描画されるトリガーは？
  - stateが変更された時
  - propsが変更された時

### useStateによるstateの宣言方法

```javascript
// useStateによるstateの宣言
// - state: 状態
// - setState: 更新のための関数
const [state, setState] = useState(initialState)

// stateの更新
setState(newState)

// 具体例
const [message, setMessage] = useState('Torahack is cool')
const [likes, setLikes] = useState(0)
```

### propsとstateの違い

- props
  - 親から渡される値
  - 子供から親に対してpropsを更新するなどはできない
- state
  - コンポーネント内で宣言、利用する値
  - stateを更新関数ごと子に渡すのはよくやること

## ライフサイクルとは

- コンポーネントが生まれてから破棄されるまでの時間のながれ
- ライフサイクルメソッドを使うと、次点に応じた処理を実行できる
- クラスコンポーネント時代には、以下の３メソッドが頻出だった
  - `componentDidMount()`
  - `componentDidUpdate()`
  - `componentWillUnmount()`
- Hooks時代は、`useEffect()`でライフサイクルを表現

### 3種類のライフサイクル

- Mounting
  - コンポーネントが配置される（生まれる）期間
    - 初期化
    - 初回レンダリング
    - マウント後の初回処理（`componentDidMount()`）
- Updating
  - コンポーネントが変更される（成長する）期間
    - 再レンダリング
    - 更新後の処理（`componentDidUpdate()`）
- Unmounting
  - コンポーネントが破棄される（死ぬ）期間
    - 破棄直前の処理（`componentWillUnmount()`）

### useEffect

- effectは副作用
- Reactにおける副作用とは **レンダリングによって引き起こされる処理** のことである
- コンポーネントが変更されたら、再描画のために`return`が行われる
- `useEffect`の中に書いた処理は、再描画のたびに実行される

### useEffectの実行タイミング

- レンダリングが行われるタイミング
- 対象のstateやpropsを指定することで、タイミングの調整も可能
  - 初回のレンダリングのみ
  - 特定のstateが変更されるたびに実行される

### クリーンナップ関数

- useEffect内で、関数をreturnする
- 再レンダリングが行われる直前に、returnしていたクリーンナップ関数が実行される

### useEffectのユースケース

- APIやデータベースから非同期通信でデータを取得(fetch)する
- 特定の値が変わったらデータを再取得(refetch)する