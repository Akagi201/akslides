
![upyun_webrtc](http://akslides.b0.upaiyun.com/upyun_webrtc.png)

## 又拍云实时音视频通信服务的技术优势

刘博 @ UPYUN

2017-08-05

---

![upyun_logo](http://akslides.b0.upaiyun.com/upyun_logo5.png)

---

## About Me

![akhead](http://akagi201.qiniudn.com/akhead.png)

* System & Media Developer at UPYUN.
* Blogger & Writer.
* Open source enthusiast.

---

## Flash?

----

<a href="https://www.statista.com/chart/3796/websites-using-flash/" title="Infographic: The Web Is Turning Its Back on Flash | Statista"><img src="https://infographic.statista.com/normal/chartoftheday_3796_websites_using_flash_n.jpg" alt="Infographic: The Web Is Turning Its Back on Flash | Statista" width="100%" height="auto" style="width: 100%; height: auto !important; max-width:960px;-ms-interpolation-mode: bicubic;"/></a>

----

* Saying goodbye to Flash in Chrome: <https://www.blog.google/products/chrome/saying-goodbye-flash-chrome/>
* Adobe 近期宣布到 2020 年停止维护 Flash: <https://blogs.adobe.com/conversations/2017/07/adobe-flash-update.html>
* GitHub 开发者向 Adobe 请愿 Flash 开源: <https://github.com/pakastin/open-source-flash>

---

## Goodbye Flash, Hello WebRTC

---

## UPYUN Weekly Meeting

* 北京, 杭州, 上海, 广州.

* 每个周一的周会.

* 需要一个远程会议系统.

----

In The Past!

![telephone](http://akslides.b0.upaiyun.com/telephone.jpg)

----

Now!

![luoji](http://akslides.b0.upaiyun.com/luoji.png)

----

## 互动直播的特点

* 互动直播是多路音视频以及数据实时通信的解决方案.
* 互动直播和传统直播相比的本质的区别是延时.
* 与传统的直播相比, 互动直播赋予了参与直播的每一个成员互动交流的能力, 因此, 也对实时性, 抗回声要求更高.
* 在视频会议, 远程教育, 远程咨询, 视频社交, 互动游戏等很多场景往往只能选择实时性更高的互动直播技术.

---

## 为什么选择 WebRTC?
* WebRTC 是一个开源, 免专利费的项目, 大大节省了我们的开发时间成本.
* WebRTC 由 Google 主导, 技术非常先进.
* 各大浏览器以及终端逐渐加大对 WebRTC 技术的支持.

----

## WebRTC Overview
* WebRTC 全称是 Web Real-Time Communication.
* WebRTC 并不是一个单一的协议, 而是一个标准, 包含一堆协议和 API.
* WebRTC 通过提供简单易用的 JavaScript APIs 让浏览器拥有了 P2P 音视频和数据分享的能力, 同时不需要安装任何插件.

----

## WebRTC Standards and History
* 2010-05, Google 花了 $68.2 million 收购了 GIPS.
* 2011-05, Google 开源了 WebRTC 项目.
* WEBRTC W3C Working Group: 浏览器 API.
* RTCWEB IETF Working Group: 协议, 数据格式, 安全, P2P 等.
* WebRTC 并不是一个孤立的协议, 起初是为了浏览器与浏览器之间实时通信, 也可以通过信令协议对接现有的 SIP 客户端, PSTN 网络, 移动端等.

----

<img src="https://akslides.b0.upaiyun.com/webrtc_audio_video_engine.png" height="500" alt="webrtc_audio_video_engine" align=center />

----

<img src="https://akslides.b0.upaiyun.com/webrtc_transports.png" height="500" alt="webrtc_transports" align=center />

---

## WebRTC Server Considerations

<img src="https://akslides.b0.upaiyun.com/webrtc_server.png" height="200" alt="webrtc_server" align=center />

---

## Signaling

<img src="https://akslides.b0.upaiyun.com/webrtc_signaling.png" height="500" alt="webrtc_signaling" align=center />

----

## Relay SDP between Clients.

<img src="https://akslides.b0.upaiyun.com/sdp_anatomy.png" height="500" alt="sdp_anatomy" align=center />

----

## Considerations Outside of WebRTC

<img src="https://akslides.b0.upaiyun.com/webrtc_out_signaling.png" height="400" alt="webrtc_out_signaling" align=center />

---

## NAT Traversal

<img src="https://akslides.b0.upaiyun.com/stun_server.png" height="600" alt="stun_server" align=center />

----

## ICE
* STUN Server.
* TURN Server.

----

## STUN Server

<img src="https://akslides.b0.upaiyun.com/stun_arch.png" height="600" alt="stun_arch" align=center />

---

## Media Server

### Peer-to-Peer vs Peer-to-Server

<img src="https://akslides.b0.upaiyun.com/peer_to_server.png" height="500" alt="peer_to_server" align=center />

----

## Media Server Advantage

<img src="https://akslides.b0.upaiyun.com/media_server_adv.png" height="600" alt="media_server_adv" align=center />

----

## Design Trade-Off

<img src="https://akslides.b0.upaiyun.com/design_tradeoff.png" height="600" alt="design_tradeoff" align=center />

----

## Multi-Party Conferencing

<img src="https://akslides.b0.upaiyun.com/multi_party_conf.png" height="500" alt="multi_party_conf" align=center />

---

## WebRTC Gateway
* HTTP/WebSocket
* SIP

---

## 我们的实时通信底层平台 UPRTC
* 传统的 WebRTC 应用模式是 P2P 的, 我们改造成服务器中转的模式.
* 完全分布式系统, 部署到全国所有边缘节点, 通过我们的内部加速网络加速.
* 网络拥塞自适应控制, 较强的弱网适应能力.
* 针对底层开源组件进行优化改造, 支持高并发.
* 灵活高效的业务信令. 支持对敏感信令进行鉴权.

----

## UPRTC 架构

![uprtc_arch](https://akslides.b0.upaiyun.com/uprtc_arch.png)

----

* utun 解决跨地区, 跨 ISP 延迟高且不稳定等网络问题.
* 覆盖 200 多个边缘节点, 4000 多台服务器.
* 覆盖 3 大运营商, 2 个小运营商.
* uprtc 实现媒体接入, 接入 Web 端与移动端.

----

## UPRTC 技术组成

<img src="https://akslides.b0.upaiyun.com/uprtc_business.png" height="500" alt="uprtc_business" align=center />

---

## 基于我们底层 UPRTC 平台的第一个项目 - 上会

----

## Web 端

<img src="https://akslides.b0.upaiyun.com/upmeeting_browser.png" height="500" alt="upmeeting_browser" align=center />

----

## 移动端

<img src="https://akslides.b0.upaiyun.com/upmeeting_ios.jpeg" height="500" alt="upmeeting_ios" align=center />

---

## 开发经验
* 我们选用的编码格式 H.264 + Opus.
* 要用自建 STUN server, 使用 Trickle Ice 加快 NAT 穿透, 建立连接过程.
* 可以不去搭建 TURN server.
* 需要做码率动态控制, 在弱网环境能正常使用. 自动根据参与人数控制总带宽在 2 Mbps以内.
* 扩展性与性能比兼容性更加重要.
* 客户端解码能力有限, 总会话人数控制在 8 人以内.

---

## Q&A

Thanks

Contribute your ideas!
