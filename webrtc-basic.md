
![webrtc_struct](http://akagi201.qiniudn.com/webrtc_struct.png)

## WebRTC Basic

@Akagi201

2017-06-26

---

本课程以代码实践为主, 理论部分也会进行介绍, 但尽量不占用过多的章节.

---

## Outline
* WebRTC 背景知识.
* WebRTC 的相关协议介绍.
* WebRTC 主要的 API 接口.

---

## Overview
* WebRTC 全称是 Web Real-Time Communication.
* WebRTC 并不是一个单一的协议, 而是一个标准, 包含一堆协议和 API.
* WebRTC 通过提供简单易用的 JavaScript APIs 让浏览器拥有了 P2P 音视频和数据分享的能力, 同时不需要安装任何插件.

---

## Standards and History
* 2010-05, Google 花了 $68.2 million 收购了 GIPS.
* 2011-05, Google 开源了 WebRTC 项目.
* WEBRTC W3C Working Group: 浏览器 API.
* RTCWEB IETF Working Group: 协议, 数据格式, 安全, P2P 等.
* WebRTC 并不是一个孤立的协议, 起初是为了浏览器与浏览器之间实时通信, 也可以通过信令协议对接现有的 SIP 客户端, PSTN 网络, 移动端等.

---

## WebRTC 的核心组成
* 音视频引擎. OPUS, VP8/VP9, H264
* 传输层协议. 底层传输协议为 UDP.
* 媒体协议. SRTP/SRTCP.
* 数据协议. DTLS/SCTP.
* P2P 内网穿透. STUN/TURN/ICE/Trickle ICE
* 信令与 SDP 协商. HTTP/WebSocket/SIP. Offer Answer 模型.

----

<img src="https://akslides.b0.upaiyun.com/webrtc_audio_video_engine.png" height="500" alt="webrtc_audio_video_engine" align=center />

----

<img src="https://akslides.b0.upaiyun.com/webrtc_transports.png" height="500" alt="webrtc_transports" align=center />

---

## 标准文档
* W3C API 相关文档: <https://github.com/w3c>, MDN
* IETF 协议相关文档: <https://datatracker.ietf.org/>

---

## Browser APIs
* MediaStream: 获取音视频流.
* RTCPeerConnection: 音视频数据通信.
* RTCDataChannel: 二进制数据通信.

---

## getUserMedia

* MediaDevices.getUserMedia()

提示用户允许使用一个视频和/或一个音频输入设备, 如果用户给予许可, 就返回一个Promise 对象. MediaStream 对象作为回调函数参数.

```
navigator.mediaDevices.getUserMedia(constraints).then(function(stream) {
  /* use the stream */
}).catch(function(err) {
  /* handle the error */
});
```

* MDN: <https://developer.mozilla.org/en-US/docs/Web/API/MediaDevices/getUserMedia>

---

## RTCPeerConnection

---

## RTCDataChannel
