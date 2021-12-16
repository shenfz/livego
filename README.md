![logo](./logo.png)

简单高效的直播服务器：
- 安装和使用非常简单；
- 纯 Golang 编写，性能高，跨平台；
- 支持常用的传输协议、文件格式、编码格式；

## 支持的传输协议
- RTMP
- AMF
- HLS
- HTTP-FLV

## 支持的容器格式
- FLV
- TS

## 支持的编码格式
- H264
- AAC
- MP3
 
## 使用
1. 启动服务：执行 `livego` 二进制文件启动 livego 服务；
2. 访问 `http://localhost:8090/control/get?room=movie` 获取一个房间的 channelkey(channelkey用于推流，movie用于播放).
3. 推流: 通过`RTMP`协议推送视频流到地址 `rtmp://localhost:1935/{appname}/{channelkey}` (appname默认是`live`), 例如： 使用 `ffmpeg -re -i demo.flv -c copy -f flv rtmp://localhost:1935/{appname}/{channelkey}` 推流([下载demo flv](https://s3plus.meituan.net/v1/mss_7e425c4d9dcb4bb4918bbfa2779e6de1/mpack/default/demo.flv));
4. 播放: 支持多种播放协议，播放地址如下:
    - `RTMP`:`rtmp://localhost:1935/{appname}/movie`
    - `FLV`:`http://127.0.0.1:7001/{appname}/movie.flv`
    - `HLS`:`http://127.0.0.1:7002/{appname}/movie.m3u8`

##所有配置项: 
```bash
./livego  -h
Usage of ./livego:
      --api_addr string       HTTP管理访问监听地址 (default ":8090")
      --config_file string    配置文件路径 (默认 "livego.yaml")
      --flv_dir string        输出的 flv 文件路径 flvDir/APP/KEY_TIME.flv (默认 "tmp")
      --gop_num int           gop 数量 (default 1)
      --hls_addr string       HLS 服务监听地址 (默认 ":7002")
      --hls_keep_after_end    Maintains the HLS after the stream ends
      --httpflv_addr string   HTTP-FLV server listen address (默认 ":7001")
      --level string          日志等级 (默认 "info")
      --read_timeout int      读超时时间 (默认 10)
      --rtmp_addr string      RTMP 服务监听地址 (默认 ":1935")
      --write_timeout int     写超时时间 (默认 10)
```
## TODO List
 > * add  API , push stream by ffmpeg 
 > * add  frontend modular, playing in browser 
 > * add  rtsp support