# Redux

- もとはJavaScript向けに定義されたアーキテクチャ
- iOS / Android でもよく用いられる状態管理手法

## 構成要素

- Store(State)
- UI
- Action
- Reducer

## Store

- Reduxを管理するオブジェクト
- Stateをプロパティとして持つ
- Actionsを実行するdispatchをメソッドとして持つ
- 状態StateはUIに反映される

## UI

- Stateを元に作成
- ユーザ操作はActionsを呼び出す

## Actions

- ユーザ操作をReducerに伝える

## Reducer

- 状態をStoreに伝える
- 引数が同じであった場合、同じ値を返す
  - 副作用のない純粋な関数
- 副作用がないので、ファイル入出力やAPIリクエストなどは行わない
  - 副作用のある処理はミドルウェアの仕事