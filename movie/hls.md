# HLSの生成

## ffmpeg を入れる

brewでffmpegをインストールする。

```sh
brew install ffmpeg
```

## m3u8ファイルの生成

```sh
ffmpeg -i input.mp4 \
  -map 0:v -map 0:a -c:v:0 libx264 -pix_fmt yuv420p -c:a:0 aac -b:a:0 128k -ar 48000 \
  -s 1920x1080 -b:v:0 5000k -maxrate 5000k -bufsize 10000k \
  -map 0:v -map 0:a -c:v:1 libx264 -pix_fmt yuv420p -c:a:1 aac -b:a:1 128k -ar 48000 \
  -s 1280x720  -b:v:1 2800k -maxrate 2800k -bufsize 5600k \
  -map 0:v -map 0:a -c:v:2 libx264 -pix_fmt yuv420p -c:a:2 aac -b:a:2 128k -ar 48000 \
  -s 854x480   -b:v:2 1400k -maxrate 1400k -bufsize 2800k \
  -f hls -hls_time 4 -hls_playlist_type vod -hls_segment_type mpegts \
  -hls_flags independent_segments \
  -var_stream_map "v:0,a:0 v:1,a:1 v:2,a:2" \
  -master_pl_name video.m3u8 \
  -hls_segment_filename "v%v/file_%03d.ts" v%v/prog_index.m3u8
```

## シングルビットレートなら

```sh
ffmpeg -i video.mp4 -c:v copy -c:a copy -f hls -hls_time 3 -hls_playlist_type vod -hls_segment_filename "video%3d.ts" video.m3u8
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


## 結合

-i の順番はどっちでも良さそう

```sh
ffmpeg -i /Users/hoshi005/Downloads/video-2024-04-06T13-32-17.369Z.ts -i /Users/hoshi005/Downloads/video-2024-04-06T13-30-22.942Z.ts -c:v copy -c:a copy -map 0:v:0 -map 1:a:0 output.mp4
```