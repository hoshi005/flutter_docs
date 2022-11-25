# ネイティブ連携

## 3つのネイティブ連携機能

- MethodChannel
- EventChannel
- MessageChannel

## MethodChannel

- ネイティブ側で定義した関数をFlutter側から呼び出すことができる
- １回の呼び出しに対して、一度のみ戻り値が返ってくる
- 単発的に情報を取得する際に用いられる

## EventChannel

- ネイティブ側からflutter側に連続的にデータを送ることができる
- flutter側でEventChannelのStreamをListenすることで、連続的に取得可能
- 主にネイティブ側で状態が変更され、それらを通知する用途で用いられる

## MessageChannel

- 双方向から連続的なデータを送ることができる
- flutter側、ネイティブ側のどちらからも連続的にデータを送り、ハンドリングできる
- PlatformViewと合わせて用いられることが多い