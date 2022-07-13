# async, await, then

## async

- 非同期メソッドの定義に利用する
- 戻り値は、`Future`でラップした値とする
    - 戻り値がない場合は`Future<Void>`が推奨されている？
- `async`がなくても、`Future`型でreturnすれば良さそう
- `async`があると、`Future`型でラップしなくても、自動的にラップしてくれる

## await

- 非同期メソッドの実行を待ってから以降の処理を実行したい場合に利用する
- `async` が定義されているメソッド内でのみ利用できる

## then

- 非同期メソッドの実行結果のコールバックを受け取って処理したい場合に利用する
- `then`の外に記述された処理はコールバックを待たずに実行されていく
- `async + await` が推奨されているみたい（ネストが減るから）

## 参考にした

- [Zenn](https://zenn.dev/iwaku/articles/2020-12-29-iwaku)
- [Keisuke Kawajiri](https://medium.com/@kawanojieee/dart-async-await-394846fb3d2c)
