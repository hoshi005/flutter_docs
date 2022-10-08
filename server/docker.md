# docker

## コマンド

![](images/docker_command.jpeg)

#### penguin という名前のイメージを pull(ダウンロード) したい場合

```bash
$ docker image pull penguin
```

#### penguin という名前のイメージを container として run したい場合

```bash
$ docker container run penguin

# 省略形もOK
$ docker run penguin
```

#### penguin という名前のイメージをコンテナとして start(開始) したい場合

```bash
$ docker container start penguin

# 省略形もOK
$ docker start penguin
```