
![live-streaming-photo](http://akagi201.qiniudn.com/akslides/live-streaming-photo.jpg)

## WebSocket & MSE for Live

[@Akagi201](https://github.com/Akagi201)

2016-12-01

---

## Outline
* HTML5 Live Streaming
* WebSocket Overview
* MSE Overview
* Demo Time

---

## HTML5 Live Streaming

当前为了满足比较火热的移动 Web 端直播需求, 一系列的 HTML5 直播技术迅速的发展了起来.

----

## HTML5 直播的关键技术

* HLS: 基于 HTTP, CDN 支持非常好, 但是延时高, 不支持互动直播场景.
* WebSocket + MSE: 基于 TCP, 实时性较好, 技术还在发展中, 不太成熟, 可用于互动直播.
* WebRTC: 基于 UDP, 实时性最好, 缺少比较成熟的开源中转服务器方案.

---

## WebSocket 协议介绍
* 基于 TCP
* RFC 6455 和 RFC 7936
* HTTP Upgrade

----

![websocket_protocol](https://akshare.b0.upaiyun.com/assets/websocket_protocol.png)

----

## WebSocket 握手

WebSocket 握手就利用了这种 HTTP Upgrade 机制. 一旦握手完成，后续数据传输就直接在 TCP 上完成.

----

## HTTP Upgrade

要发起 HTTP/1.1 协议升级，客户端必须在请求头部中指定这两个字段:

```
Connection: Upgrade
Upgrade: protocol-name[/protocol-version]
```

----

如果服务端同意升级, 那么需要这样响应:

```
HTTP/1.1 101 Switching Protocols
Connection: upgrade
Upgrade: protocol-name[/protocol-version]

[... data defined by new protocol ...]
```

可以看到, HTTP Upgrade 响应的状态码是 `101`, 并且响应正文可以使用新协议定义的数据格式.

---

## WebSocket JavaScript API 介绍

目前主流的浏览器提供了 WebSocket 的 API 接口, 可以发送消息(文本或者二进制)给服务器, 并且接收事件驱动的响应数据.

----

## Step1 检查浏览器是否支持 WebSocket.

```
if(window.WebSocket) {
	// WebSocket代码
}
```

----

## Step2 建立连接

```
var ws = new WebSocket('ws://localhost:8327');
```

----

## Step3 注册回调函数以及收发数据

* 分别注册 WebSocket 对象的 onopen, onclose, onerror 以及 onmessage 回调函数.

* 通过 `ws.send()` 来进行发送数据, 这里不仅可以发送字符串, 也可以发送 Blob 或 ArrayBuffer 类型的数据.

* 如果接收的是二进制数据，需要将连接对象的格式设为 blob 或 arraybuffer.

```
ws.binaryType = 'arraybuffer';
```

---

## WebSocket Golang API 介绍

* [`golang.org/x/net/websocket`](https://godoc.org/golang.org/x/net/websocket)
* 与 `net/http` 结合较好, 方便一起使用.

----

* websocket 的 API 使用非常简单, 基本和 TCP 的接口类似.

* 可以将 websocket 的 handler function 通过 `websocket.Handler` 转换成 `http.Handler`, 这样就可以跟 `net/http` 库一起使用了.

* 然后通过 `websocket.Message.Receive` 来接收数据, 通过 `websocket.Message.Send` 来发送数据.

---

## MSE

* MSE 是为了解决什么问题而诞生的?

* 在介绍 MSE 之前, 我们先看看 HTML5 `<audio>` 和 `<video>` 有哪些限制.

----

### HTML5 `<audio>` 和 `<video>` 标签的限制
* 不支持流.
* 不支持 DRM 和加密.
* 很难自定义控制, 以及保持跨浏览器的一致性.
* 编解码和封装在不同浏览器支持不同.

----

MSE 是解决 HTML5 的流问题.

----

## MSE 介绍
* 主流浏览器支持的新的 Web API.
* JavaScript 传输媒体流片段到一个 HTMLMediaElement.
* 无插件.

----

## 不同平台都在开放底层多媒体操作 API

* Flash 平台有 Netstream
* Android 平台有 Media Codec API
* Web 上对应的就是标准的 MSE

----

## Browser Support

* 通过 [caniuse](http://caniuse.com/#feat=mediasource) 来检查是否浏览器支持情况.
* 通过 [`MediaSource.isTypeSupported()`](https://developer.mozilla.org/en-US/docs/Web/API/MediaSource/isTypeSupported) 可以进一步地检查 codec MIME 类型是否支持.

![mse-support](https://akshare.b0.upaiyun.com/assets/mse-support.png)

----

## 视频封装格式
* WebM: WebM 和 WebP 是两个姊妹项目, 都是由 Google 赞助的. 由于 WebM 是基于 Matroska 的容器格式, 所以天生是流式的, 很适合用在流媒体领域里.
* fMP4

----

## fMP4
* fMP4 由一系列的片段组成.
* 支持 byte-range 请求.

----

## MP4 Tools

* [gpac](https://gpac.wp.mines-telecom.fr/) 原名 mp4box, 是一个媒体开发框架, 在其源码下有大量的媒体分析工具可以使用, [testapps](https://github.com/gpac/gpac/tree/master/applications/testapps)
* [mp4box.js](http://download.tsi.telecom-paristech.fr/gpac/mp4box.js/filereader.html) 是 mp4box 的 Javascript 版本.
* [bento4](https://www.bento4.com/) 一个专门用于 MP4 的分析工具.
* [mp4parser](http://mp4parser.com/) 在线 MP4 文件分析工具.

----

## fragment mp4 vs non-fragment mp4

----

下面一个 fragment mp4 文件通过 [mp4parser](http://mp4parser.com/) 分析后的截图

![fmp4](https://akshare.b0.upaiyun.com/assets/fmp4.png)

----

下面一个 non-fragment mp4 文件通过 [mp4parser](http://mp4parser.com/) 分析后的截图

![nfmp4](https://akshare.b0.upaiyun.com/assets/nfmp4.png)

----

* 在今年的 WWDC 大会上宣布会在 iOS 10, tvOS, macOS 的 HLS 中支持 fMP4.

* 值得一提的是, fMP4, CMAF, ISOBMFF 其实都是类似的东西.

----

## MSE 内部结构

![mse_arch](http://akshare.b0.upaiyun.com/assets/mse_arch.png)

----

## Codec MIME

```
MediaSource.isTypeSupported('audio/mp3'); // false
MediaSource.isTypeSupported('video/mp4'); // true
MediaSource.isTypeSupported('video/mp4; codecs="avc1.4D4028, mp4a.40.2"'); // true
```

----

## 获取 Codec MIME string 方法

* [mp4info](http://nickdesaulniers.github.io/mp4info/)
* `mp4info test.mp4 | grep Codecs`


----

可以得到类似如下结果:

```
❯ mp4info fmp4.mp4| grep Codec
    Codecs String: mp4a.40.2
    Codecs String: avc1.42E01E
```

----

## 检查一个 MP4 是否已经 fragment

```
mp4dump test.mp4 | grep "\[m"
```

----

## 将 non-fragment MP4 转换成 fragment MP4

* 使用 FFmpeg 的 `-movflags` 来转换
* mp4fragment

---

## MSE JavaScript API 介绍

从高层次上看, MSE 提供了

* 一套 JavaScript API 来构建 media streams.
* 一个拼接和缓存模型.
* 不依赖任何特定的封装格式和编解码格式.
* 识别一些 byte 流类型:
  * WebM
  * ISO Base Media File Format
  * MPEG-2 Transport Streams

---

## Demo1: 点播

后端读取一个 fmp4 文件, 通过 WebSocket 发送给 MSE, 进行播放.

---

## Demo2: 直播

后端代理一条 http-flv 直播流, 通过 WebSocket 发送给 MSE, 进行播放.
