
![live-streaming-photo](https://akslides.b0.upaiyun.com/live-streaming-photo.jpg)

## WebRTC Overview

@Akagi201

2016-07-18

---

## RTMP/HLS
* <https://github.com/nareix/joy4> 参考 ffmpeg 的架构, 修改灵活, 欠缺稳定性, 日志, 动态配置方面.

---

## WebRTC/WebSockets

* websocket 方案: <http://instant-webcam.com/> 前端js解码

---

### WebRTC API 3类
* MediaStream: 获取音频和视频流, 与网络无关.
* RTCPeerConnection: 音频和视频数据通信, 基于 UDP.
* RTCDataChannel: 任意应用数据通信, 基于 UDP.

---

### 架构图

```
+-----------------------+-------------------------+
|   RTCPeerConnection   |      RTCDataChannel     |
+-----------------------+-------------------------+
|          SRTP         |           SCTP          |
+             +---------+-------------------------+
|             |                DTLS               |
+-------------+-----------------------------------+
|                ICE, STUN, TURN                  |
+-------------------------------------------------+
|                       UDP                       |
+-------------------------------------------------+
|                       IP                        |
+-------------------------------------------------+
```

---

### 协议
* SCTP: 建立在 UDP 之上的 TCP
* DTLS: UDP 版的 TLS
* UDP
* ICE: 用于建立端到端通道, 优先直连, 其次STUN协商, 再次TURN转发.
* SRTP/SRTCP 对应安防领域常用的 RTP/RTCP 的安全版本.

----

### 架构
* P2P 模式
* MCU/SFU 模式

---

### 开源
* STUN: stuntman <http://www.stunprotocol.org/>

----

#### C
* <https://github.com/meetecho/janus-gateway> 更新快.
* <https://github.com/ging/licode> 整套方案, 有nodejs API.
* <https://github.com/Kurento/kms-core> 更新快.

----

#### Go
* <https://github.com/keroserene/go-webrtc>
* <https://github.com/strukturag/spreed-webrtc>

----

#### Rust
* <https://github.com/openansible>

---

## Q&A

Thanks

Contribute your ideas!
