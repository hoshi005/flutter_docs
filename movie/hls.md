# HLSの生成

## ffmpeg を入れる

brewでffmpegをインストールする。

```sh
brew install ffmpeg
```

## m3u8ファイルの生成

```sh
# 基本形。でもこれではダメっぽい
ffmpeg -i video.mp4 video.m3u8

# これでいける
ffmpeg -i video.mp4 -c:v copy -c:a copy -f hls -hls_time 9 -hls_playlist_type vod -hls_segment_filename "video%3d.ts" video.m3u8
```

## firebaseの用意

既にあるプロジェクトのローカルディレクトリを作る

```sh
firebase login

firebase init

# このあと、スペースキーでhostingを選択して、Enter
```

## 注意

ローカルのディレクトリをアップロードしたら、既存のファイルが消えたりするので注意。

