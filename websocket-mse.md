
![live-streaming-photo](http://akslides.b0.upaiyun.com/live-streaming-photo.jpg)

## WebSocket & MSE for Live

@Akagi201

2016-11-30

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

## 关键技术

* HLS
* WebSocket + MSE
* WebRTC

---

## WebSocket 协议介绍
* 基于 TCP
* RFC 6455 和 RFC 7936
* HTTP Upgrade

----

![websocket_protocol](http://akshare.b0.upaiyun.com/assets/websocket_protocol.png)

---

## WebSocket JavaScript API 介绍

---

## WebSocket Golang API 介绍

---

## MSE 介绍
* 主流浏览器支持的新的 Web API.
* JavaScript 传输媒体流片段到一个 HTMLMediaElement.
* 无插件.

----

## HTML5 `<video>` `<audio>` 标签限制
* 不支持流.
* 不支持 DRM 和加密.
* 很难自定义控制, 以及保持跨浏览器的一致性.
* 编解码和封装在不同浏览器支持不同.

---

## MSE JavaScript API 介绍

----

## 从高层次上看, MSE 提供了

* 一套 JavaScript API 来构建 media streams.
* 一个拼接和缓存模型.
* 识别一些 byte 流类型:
  * WebM
  * ISO Base Media File Format
  * MPEG-2 Transport Streams

---

## Demo1: 点播

后端读取一个 fmp4 文件, 通过 WebSocket 发送给 MSE, 进行播放

---

## Demo2: 直播

后端代理一条 http-flv 直播流, 通过 WebSocket 发送给 MSE, 进行播放
