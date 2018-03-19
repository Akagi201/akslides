
![webrtc_cover](http://akagi201.qiniudn.com/akslides/webrtc_cover.png)

## WebRTC Introduction

@Akagi201

2017-06-01

---

## About Me
* 从传统的安防, 到传统的 RTMP 直播, 再到最新的 WebRTC.
* Go, C/C++, Web 开发.
* 最近对数字货币跟区块链比较感兴趣.
* <http://akagi201.org>

---

## Outline
* 简介
* 标准与历史
* 音视频引擎
* 实时传输层协议
* 信令与 SDP 协商
* 音视频通道: SRTP 与 SRTCP
* 数据通道: SCTP
* 浏览器接口
* WebRTC 应用与性能

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

## Audio and Video Engines
* 访问系统硬件来获取音视频.
* 仅仅是能获取跟传输音视频流是远远不够的, 还需要做很多的优化工作.
* OPUS, VP8, VP9, H.264.

----

<img src="http://akagi201.qiniudn.com/akslides/webrtc_audio_video_engine.png" height="500" alt="webrtc_audio_video_engine" align=center />

---

## 实时传输层协议
* 底层是 UDP 协议.
* 应用与编解码要容忍间歇性丢包, 填充小的数据丢失, 而不影响音视频质量.
* 低延时比可靠性更重要.

----

## UDP 的特点
* 不保证消息送达. 没有 ack, 重传, 超时.
* 不保证传输顺序. 没有包序号, 没有重排, 没有队首阻塞.
* 没有连接状态跟踪. 不维护连接状态的状态机.
* 没有拥塞控制. 没有自带的网络反馈机制.

----

<img src="http://akagi201.qiniudn.com/akslides/webrtc_transports.png" height="500" alt="webrtc_transports" align=center />

---

## Signaling and Session Negotiation
* SDP 文本协议
* Offer-Answer 模型
* NAT 穿透

----

## SDP 文本协议

```
(... snip ...)
m=audio 1 RTP/SAVPF 111 ... // 音频
a=extmap:1 urn:ietf:params:rtp-hdrext:ssrc-audio-level
a=candidate:1862263974 1 udp 2113937151 192.168.1.73 60834 typ host ... // 候选地址与协议
a=mid:audio
a=rtpmap:111 opus/48000/2 // codec 编码与配置
a=fmtp:111 minptime=10
(... snip ...)
```

----

## Offer-Answer 模型

![webrtc_offer_answer](http://akagi201.qiniudn.com/akslides/webrtc_offer_answer.png)

----

## NAT 穿透
* STUN / TURN server
* ICE agent 获取本地 IP 端口, 通过 STUN server 获取外网映射后的 IP 端口.
* ICE agent 负责两个 peer 之间的连接性检查.
* ICE agent 负责发送 keepalive 保活包.

----

## Trickle ICE
* 两个 peer 立即交换不带 ICE 候选地址的 SDP 信息.
* ICE 候选地址在获取后立即通过信令通道传递给对端.
* ICE 连接检查在获取候选地址后立即进行.

---

## 音视频通道: SRTP 和 SRTCP
* 应用层是不需要对怎样传输音视频进行优化与调整的.
* WebRTC 内核自己实现了网络拥塞控制算法, 每个连接先从一个较低码率开始, 然后逐渐提升, 达到带宽的最大值.
* 音视频引擎跟网络引擎会动态调整音视频质量来动态调整码率, 根据网络抖动, 丢包, 网络带宽等.

----

## SRTP
* 每个 SRTP 包包含一个自增的序号. 帮助接收端检测与考虑乱序问题.
* 每个 SRTP 包包含一个时间戳. 采样时间. 通常用于音视频同步.
* 每个 SRTP 包包含一个 SSRC ID. 作为 stream ID, 用于关联每一个包到一个独立的流.

----

![srtp](http://akagi201.qiniudn.com/akslides/srtp.png)

----

## SRTCP
* SRTCP 负责可每个独立的 SRTP 包的传输控制, 一个独立的对于每条流的反馈通道.
* SRTCP 跟踪发送和丢包, 最后接收的包序号, 每个 SRTP 的内部 jitter 和其他 SRTP 统计信息.
* 两端 peer 周期性的交互这些信息, 来调整发送码率, 编码质量等其他流信息.

---

## 数据通道: SCTP
* 应用层传输任意二进制数据通过 DataChannel, DataChannel 使用 SCTP 协议.
* SCTP 运行在 DTLS 通道之上.

----

## SCTP
* 支持多路复用多个独立的 channel.
* 每个 channel 支持顺序和乱序传输.
* 每个 channel 支持可靠和不可靠传输.
* 每个 chennel 都有一个由应用定义的优先级.
* 提供面向消息的 API, 每个消息可以被传输层分片和重组.
* 实现流和拥塞控制机制.
* 跟 HTTP/2 很像.

----

![sctp](http://akagi201.qiniudn.com/akslides/sctp.png)

----

<img src="http://akagi201.qiniudn.com/akslides/websocket_vs_datachannel.png" height="500" alt="websocket_vs_datachannel" align=center />

---

### Browser APIs
* MediaStream: 获取音视频流.
* RTCPeerConnection: 音视频数据通信.
* RTCDataChannel: 二进制数据通信.

---

## WebRTC 应用与性能
* P2P vs Central
* MCU vs SFU

----

![webrtc_arch](http://akagi201.qiniudn.com/akslides/webrtc_arch.png)

----

![mcu_vs_sfu](http://akagi201.qiniudn.com/akslides/mcu_vs_sfu.png)

---

## Q&A

Thanks

Contribute your ideas!
