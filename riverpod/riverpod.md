# Riverpod

- [公式ドキュメント](https://riverpod.dev/ja/docs/getting_started)が日本語で充実している

## プロバイダの種類

- Provider
- StateProvider
- FutureProvider
- StreamProvider
- StateNotifierProvider
- ChangeNotifierProvider
  - あまり利用をお勧めされていない

## プロバイダの修飾子

- `.autoDispose`
  - プロバイダの監視が終わったタイミングで、プロバイダで自動にステートを破棄させることができるようになる.
- `.family`
  - プロバイダ外部の値を用いてプロバイダを作成できるようになる.