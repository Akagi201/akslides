
![upyun_webrtc](http://akslides.b0.upaiyun.com/upyun_webrtc.png)

## 实时流媒体服务器 UPRTC 介绍

UPMEDIA

2017-08-31

---

## Flash?

----

<a href="https://www.statista.com/chart/3796/websites-using-flash/" title="Infographic: The Web Is Turning Its Back on Flash | Statista"><img src="https://infographic.statista.com/normal/chartoftheday_3796_websites_using_flash_n.jpg" alt="Infographic: The Web Is Turning Its Back on Flash | Statista" width="90%" height="auto" style="width: 90%; height: auto !important; max-width:960px;-ms-interpolation-mode: bicubic;"/></a>

----

* Saying goodbye to Flash in Chrome: <https://www.blog.google/products/chrome/saying-goodbye-flash-chrome/>
* Adobe 近期宣布到 2020 年停止维护 Flash: <https://blogs.adobe.com/conversations/2017/07/adobe-flash-update.html>
* GitHub 开发者向 Adobe 请愿 Flash 开源: <https://github.com/pakastin/open-source-flash>

---

## Goodbye Flash, Hello WebRTC

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

<img src="https://akslides.b0.upaiyun.com/stun_server.png" height="500" alt="stun_server" align=center />

----

## ICE
* STUN Server.
* TURN Server.

----

## STUN Server

<img src="https://akslides.b0.upaiyun.com/stun_arch.png" height="500" alt="stun_arch" align=center />

---

## Media Server

### Peer-to-Peer vs Peer-to-Server

<img src="https://akslides.b0.upaiyun.com/peer_to_server.png" height="400" alt="peer_to_server" align=center />

----

## Media Server Advantage

<img src="https://akslides.b0.upaiyun.com/media_server_adv.png" height="500" alt="media_server_adv" align=center />

----

## Design Trade-Off

<img src="https://akslides.b0.upaiyun.com/design_tradeoff.png" height="500" alt="design_tradeoff" align=center />

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

## 交互式音视频 QoS 保障技术

@严燕冬

---

* QoS
* RTP/RTCP
* 抗丢包
* 网络拥塞控制
* 关键帧请求
* Jitter buffer

---

## Qos 概念


![qos_qoe](https://upmedia.b0.upaiyun.com/assets/qos/qos_qoe.png)


影响实时音视频质量的主要因素包括：带宽、延时、抖动、丢包。Qos（Quality of Service）就是为处理这些问题而生.

---

## 传统流媒体传输方案

<img src="https://upmedia.b0.upaiyun.com/assets/qos/no_qos.png" height="500" alt="no_qos" align=center />

---

## QoS 保障传输方案

<img src="https://upmedia.b0.upaiyun.com/assets/qos/feed_back.png" height="500" alt="feed_back" align=center />

---

## RTP

交互式实时视频应用通常采用 RTP 协议进行音视频传输，RTP头部提供了诸如负载类型、时间戳、序列号和同步源等信息保证基本的音视频实时传输需求。(RFC3550)

![qos_qoe](https://upmedia.b0.upaiyun.com/assets/qos/rtp_header.png)

---

## Rtcp

* SR：发送者报告，描述作为活跃发送者成员的发送和接收统计数字.
* RR：接收者报告，描述非活跃发送者成员的接收统计数字.

---

## 抗丢包

* 丢包重传(ARQ)
* 前向纠错(FEC)
* 丢包隐藏(PLC)

---

### 丢包重传(ARQ)

否定应答(NACK): 发送者通过接受者的反馈得知有报文在传输过程中有丢失，重传该报文。(RFC4585)

该方法的缺点是增大了端到端的延迟，尤其在丢包大量发生时更为明显。

---

#### 前向纠错(FEC)

![qos_qoe](https://upmedia.b0.upaiyun.com/assets/qos/fec.jpg)

* 在编码发送端发送冗余数据，解码端根据该冗余数据，对丢失的码流进行恢复.(RFC6363)
* 该方法的优点是视频延迟低，但发送冗余包占用了额外的带宽资源。

---

### 丢包隐藏(PLC)

* Packet Loss Concealment, 属于后向纠错, PLC 算法多数基于接收端处理, 不需要发送端参与。
* PLC 算法利用丢失信包的前一信包或邻接信包（在后一信包可获得的情况下）预测丢失的数据包. 丢包隐藏技术这类技术适用于相对小的丢包率( 有研究者说是小于 15%)和 小 长 度 的 包(4~40ms).

---

#### Opus PLC 模块

```
int WebRtcOpus_Decode(OpusDecInst* inst, const uint8_t* encoded,
                      size_t encoded_bytes, int16_t* decoded,
                      int16_t* audio_type) {
  int decoded_samples;

  if (encoded_bytes == 0) {
    *audio_type = DetermineAudioType(inst, encoded_bytes);
    decoded_samples = WebRtcOpus_DecodePlc(inst, decoded, 1);
  } else {
    decoded_samples = DecodeNative(inst,
                                   encoded,
                                   encoded_bytes,
                                   kWebRtcOpusMaxFrameSizePerChannel,
                                   decoded,
                                   audio_type,
                                   0);
  }
  if (decoded_samples < 0) {
    return -1;
  }

  /* Update decoded sample memory, to be used by the PLC in case of losses. */
  inst->prev_decoded_samples = decoded_samples;

  return decoded_samples;
}

```

---

## 网络拥塞控制

### 基于丢包

* 丢包率与带宽有时没有直接关系，导致误判。即丢包很多时候并非由于网络带宽不够用；
* 历史估计未来，缺乏预判性。假定丢包是因为带宽不够用导致，等感知到丢包，说明网络已经拥塞，这将导致视频卡顿等问题；
* 通过感知到丢包到应用层才去策略，需要一定的时间，这段时间将进一步导致拥塞。这在对延迟要求高的场景下，效果不理想。

---

<img src="https://upmedia.b0.upaiyun.com/assets/qos/loss_estimate.png" height="600" alt="loss_estimate" align=center />

---

### 基于延时

接收端采用 Google Congestion Control 算法，即 [GCC](https://tools.ietf.org/html/draft-alvestrand-rtcweb-congestion-02).

<img src="https://upmedia.b0.upaiyun.com/assets/qos/gcc_estimate.png" height="500" alt="gcc_estimate" align=center />

---


GCC 算法处理流程

![qos_qoe](https://upmedia.b0.upaiyun.com/assets/qos/gcc_process.png)

---

![qos_qoe](https://upmedia.b0.upaiyun.com/assets/qos/gcc_ts_delta.png)

* d(i) = t(i) – t(i-1) – (T(i) – T(i-1))
* dL(i) = L(i) - L(i-1)
* 延时估算模型： d(i) = dL(i) / C(i) + m(i) + v(i)    

---

* dL(i) 表示帧 i 和帧 i-1 的长度之差，
* C(i) 表示信道传输速率，
* m(i) 表示帧 i 的网络排队时延，
* v(i) 表示测量噪声，其协方差为 R。
其中 [1/C(i) m(i)] 是我们要求的目标值，即信道传输速率和网络排队时延。

---

* 构建卡尔曼滤波模型, 估算出 m(i)
* 网络状态检测用当前网络延迟 m(i) 和阈值(动态更新) 进行比较，判断出overuse，underuse 和 normal 三种网络状态之一.
* 码率控制模块维护三种码率变化趋势(Hold, Increase, Decrease),估算真正的码率 Ar.
* 当码率变化趋势为 Increase 时，当前码率为上次码率乘上系数 1.05；当码率变化趋势为 Decrease，当前码率为过去 500ms 内的最大接收码率乘上系数 0.85。当码率变化趋势为 Hold 时，当前码率保持不变。

---

```
   State ---->  | Hold      |Increase    |Decrease
   Signal-----------------------------------------
     v          |           |            |
   Over-use     | Decrease  |Decrease    |
   -----------------------------------------------
   Normal       | Increase  |            |Hold
   -----------------------------------------------
   Under-use    |           |Hold        |Hold
   -----------------------------------------------

```

---

## 关键帧请求

关键帧也叫做帧内刷新帧，简称 IDR 帧。请求方式分为：

* RTCP FIR反馈（Full intra frame request)
* RTCP PLI反馈（Picture Loss Indictor）

UPRTC 通过关键帧请求实现秒开的功能。

![qos_qoe](https://upmedia.b0.upaiyun.com/assets/qos/I_frame.png)


---

## 抖动、乱序

* jitter buffer 主要用于修正抖动, 乱序, 但同时也会与其他的 qos 策略紧密相连。当有丢包则可请求 nack, 丢帧则请求 Fir.
* 调整 jitter buffer 将牺牲延时为代价, 需要在延时和丢包、抖动之间做出平衡。

---

![qos_qoe](https://upmedia.b0.upaiyun.com/assets/qos/jitter_buffer.jpg)

---

## 结语

* QOS保障技术，不同的技术对于不同的网络状况效果不同，比如 ARQ 重传在小丢包和较低网络延迟的网络情况下能够达到较理想的效果, 音视频 QOS 的关键问题是如何能够整合这些技术，使得各个技术能够发挥到最佳效果，从而提高音视频的体验。
* 在互联网上为实时交互式音视频应用提供 QoS 保证仍是一项挑战，需要音视频编码器、传输、预处理等多模块的协作配合，或利用现有网络协议和设备的支持，才能提供给客户更多的选择和服务保证。

---

## 对接 UPRTC: WebRTC 信令

@万斌斌

---

## 信令
一系列业务及标准得以实现的载体
端到端建立通讯

* 开始/结束通话
* 处理错误的消息
* 业务控制/报告消息

---

## webrtc 信令相关标准

信令方法和协议都不由WebRTC标准来指定，而由 jsep 来概述，包括：

* 媒体能力协商(媒体类型、编解码器、媒体控制)

* p2p 信息 (网络数据，对方的公网IP、端口、内网IP及端口)

    ```
    格式:
    {                      
        "type":"offer",   // type: offer/answer            
        "sdp" : "..."     // 描述 sdp 字符串，详见 RFC 2327
    }
    ```

---

## webrtc 为何不实现信令

为了避免冗余和最大化兼容已经确立的技术

不同的应用可能会使用不同的协议，比如已经存在的SIP或者Jingle呼叫协议等。

---

## 信令实现选择：
* 标准信令协议
* 通用协议
* 数据通道专有网络

----

### 标准信令协议

例如SIP/jingle；

标准信令协议提供完整的的基础信令状态机

![信令状态机](http://upmedia.b0.upaiyun.com/assets/signal_state.svg)

----

### 通用协议

例如Http 或 Websocket 等通用传输协议。

需要重新实现标准信令所具备的功能。

----

### 数据通道专有网络 DataChannel

优点:
```
1) 降低延时。
2) 减少服务资源消耗，对服务器的要求少。
3) 保护隐私。
```

缺点:
```
1) 可能会占用成员资源。
2) 成员不稳定会到导致信令传输打断。
```

---

## uprtc 信令结构

<img src="http://upmedia.b0.upaiyun.com/assets/uprtc_signaling.svg" height="500" alt="uprtc_signaling" align=center />

---

### 信令鉴权
白名单 + 签名认证
```                      
"authorization": {
    "sign": "bAZ0B1y914RLtWvi6WU2fRCOFlY=",
    "payload": "transaction=UjEJrk6TAFWN",
    "timestamp":1490681705000000,
}
```
`<sign> = urlsafe Base64 (HMAC-SHA1 (<key>，<payload>)`

---

### 信令容器
格式:
```
  "body":{                       
    "request":"notify",        // message 请求类型                  
    "action" : "main_screen"   // 该字段用于理解该信令的含义             
    "notify_list" : [          // 通知列表
    111,
    222,                       
    ...],
    "msg" : {                  // uprtc 无需关心，有具体应用定义
        ...
    }
  }

信令容器: uprtc仅做转发，无需理解该信令

```

---

## 总结：
信令的设计 需要结合 标准、架构、性能、可拓展性 综合考虑评估

---

## Q&A

Thanks

Contribute your ideas!
