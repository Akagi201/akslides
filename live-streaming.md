
![live-streaming-photo](http://akagi201.qiniudn.com/akslides/live-streaming-photo.jpg)

## Live Streaming Overview

@Akagi201

2016-01-08

---

## Outline
* About Me
* 我的一些背景技能, 以及我欠缺的技能
* 我们在做什么?
* 流媒体的过去与现在对比
* 流媒体服务器的现状
* 流媒体协议的未来
* 流媒体开发中会遇到的问题

---

## About Me
* <http://akagi201.org>
* 高清摄像机IPC -> 路由器 -> RTMP/HLS直播 -> Python(WebSocket/Pyramid)
* 各种新技术都会玩一下.
* 比较喜欢的语言(排名有先后): Python, Javascript, Go, Lua, C.
* 其他爱好: 动漫, 日麻, 股票.
* 比较不懂: 之前大多是做单机应用的开发, 比较不懂集群, 分布式, 网络架构.

----

## OpenResty真的很赞!
* OpenResty Playground

----

## 来瞅一眼安防领域的流媒体

----

## 视频编码
* MPEG-4
* H.264/AVS
* H.265/HEVC

----

## 音频编码
* G.711
* G.726
* AAC(版权, 民用, 为了HLS)

----

![audio-quality](http://akagi201.qiniudn.com/akslides/audio-quality.png)

----

## 封装

![h264-encapsulation](http://akagi201.qiniudn.com/akslides/h264-encapsulation.jpg)

----

## 安防里领域使用的流媒体协议
* RTP/RTCP/RTSP
* 普遍存在的私有协议 / 预研DASH
* 民用: P2P/HLS

----

## RTP
* RTP(Real-time Transport Protocol) 是用于Internet上针对多媒体数据流的一种传输协议. RTP被定义为在一对一或一对多的传输情况下工作, 其目的是提供时间信息和实现流同步. RTP通常使用UDP来传送数据, 但RTP也可以在TCP或ATM等其他协议之上工作.
* RTP本身并没有提供按时发送机制或其它服务质量(QoS)保证, 它依赖于低层服务去实现这一过程. RTP并不保证传送或防止无序传送, 也不确定底层网络的可靠性.
* 传输层协议: TCP, UDP, multi-cast, http.

----

## UDP
* 无连接协议, 只受应用软件生成数据的速率, 传输带宽, 源端和终端主机性能的限制.

## TCP
* 流量控制上, 采用滑动窗口协议, 有自己的拥塞控制.

----

## RTCP
* 在RTP会话期间, 每个会话参与者周期性地向所有其他参与者发送RTCP控制信息包.

----

<img src="http://akagi201.qiniudn.com/akslides/rtp-rtcp.png" width="260" height="500" alt="rtp-rtcp" align=center />

----

## RTCP
* RTCP的主要功能是为应用程序提供会话质量或者广播性能质量的信息. 每个RTCP信息包封装发送端和/或者接收端的统计报表. 这些信息包括发送的信息包数目, 丢失的信息包数目和信息包的抖动等情况, 这些反馈信息反映了当前的网络状况, 对发送端, 接收端或者网络管理员都非常有用.
* RTCP为每个RTP用户提供了一个全局唯一的称为规范名称(Canonical Name)的标志符CNAME, 接收者使用它来追踪一个 RTP进程的参加者. 当发现冲突或程序重新启动时, RTP中的同步源标识符SSRC可能发生改变, 接收者可利用CNAME来跟踪参加者.

----

* 前2个功能均要求会议的参与者发送RTCP包. 所以, 发送速率应该得到控制以适应有大规模参与者的RTP会话. 每个参与者必须可以独立地知道会话的参与者数量, 来决定发包的速率.

----

## RTP选择UDP提供传输, 提供

* 负载类型
* 序列号
* 时间戳

----

## RTCP提供

* 数据传输的质量反馈
* 会话成员的身份识别
* 多种媒体间(音视频)的同步

----

## RTSP
* Real Time Streaming Protocol
* 是用来建和控制一个或多个时间同步的连续音视频媒体流的会话协议. 通过在客户机和服务器之间传递 RTSP 会话命令, 可以完成诸如请求播放, 开始, 暂停, 查找, 快进和快退等VCR控制操作. 虽然, RTSP 会话通常承载于可靠的 TCP 连接之上, 但也可以使用 UDP 等无连接协议来传送 RTSP 会话命令.

----

## RTSP

* 流媒体控制协议.
* 媒体数据使用RTP, RTCP协议, 一般使用UDP作为传输层.
* 在广域网容易产生丢包, 时延, 抖动.
* 适合IPTV场景, 因为IPTV使用专线.

---

# What are we doing?

----

## 移动互联网视频应用场景

* 视频直播
* P2P视频
* 视频会议

----

## 两个功能
* 流媒体源站(Origin + Transfer + Edge)
* 流媒体分发加速(RTMP分发 + HTTP-FLV + 已有HLS)

----

## 业务模式
* 纯反向代理
* 分发业务
* 全业务

----

## 纯反向代理
* 客户做源站, 流媒体集群可以配置直接回客户源站, 可通过rtmp或者http-flv回源. HTTP 集群也可以支持, 也就是 HLS 支持(又拍现有系统). RTMP, FLV 和 HLS 独立分发.

----

## 分发业务
* 客户做源站, 又拍可以将客户的 RTMP 流拉到集群, 以 RTMP, FLV, HLS 分发. 其中, HLS 分发是依靠又拍现有系统.

----

## 全业务
* 又拍做源站, 客户没有源站服务器, 客户可以将流推送到又拍, 以 RTMP, FLV, HLS 分发. 其中, HLS 分发依靠又拍现有系统.

---

## Streaming Media History

![streaming-media-history](http://akagi201.qiniudn.com/akslides/streaming-media-history.png)

---

## Live Streaming Protocols
* RTMP
* HTTP-FLV
* HLS

----

## RTMP vs HLS

![rtmp-vs-hls](http://akagi201.qiniudn.com/akslides/rtmp-vs-hls.png)

----

## RTMP
* Marcomedia公司提出的协议, 后被Adobe收购.
* RTMP协议既可以传送控制协议, 又可以传送数据协议.
* 基于TCP传输层, 保证数据不会丢失.

----

<img src="http://akagi201.qiniudn.com/akslides/rtmp-push.png" width="576" height="685" alt="rtmp-push" align=center />

----

<img src="http://akagi201.qiniudn.com/akslides/rtmp-play.png" width="662" height="668" alt="rtmp-play" align=center />

----

## HLS
* 苹果提出的基于HTTP的实时流式传输协议.
* H.264 + AAC
* MPEG-2 TS
* 流分割器(Stream Segmenter): 一系列连续, 长度均等的小TS文件.
* m3u8: 索引文件可以看作是已个连续媒体流中的播放列表滑动窗口, 每生成一个新的TS文件, 这个索引文件的内容也被更新, 新的文件 URI(统一资源定位符)加入到滑动窗 的末尾, 老的文件 URI 则被移去, 这样索引文件中将始终包含最新的固定数量的 x 个分段.
* 一般保持3个分片地址, 整体延迟比较长.

----

![streaming-protocol-compare](http://akagi201.qiniudn.com/akslides/streaming-protocol-compare.png)

---

## 直播服务器功能
* 媒体消息转发.
* 信令控制.
* 不同协议转换, 转码.
* 发布订阅模式, 支持大量订阅端接入.

----

## 直播服务器比较

![streaming-server-compare](http://akagi201.qiniudn.com/akslides/streaming-server-compare.png)

----

![streaming-servers](http://akagi201.qiniudn.com/akslides/streaming-servers.png)

----

## nginx-rtmp vs srs

* <https://github.com/ossrs/srs/wiki/v1_EN_Compare>

---

## Modern Live Streaming Protocols
* DASH
* RTMFP
* WebRTC

---

## 挑战
* 实时性(发包的延迟, 播放的延迟)
* 网络抖动
* 网络拥塞, 丢包

---

## 延迟 Delay
* 延迟指稳定网络下, 发送和接收时差.
* 转发环节越多, 延迟越大.
* 可计算.
* 物理延迟.
* 逻辑延迟. 长短接+TCP慢启动. 长连接(延迟降低275%).

---

## 抖动Jitter
* 突发的转发速度变化.
* 增加后续播放的延迟.
* 无法预先计算.
* <https://github.com/ossrs/srs/wiki/v1_CN_LowLatency>

---

## 推流端
* 编解码器: h264 + aac
* 开源软件: OBS, FMLE(Flash Media Live Encoder)

---

## 播放端
* PC端: VLC, Flash网页
* 手机H5: 通过RTMP转HLS
* 手机APP端: ffmpeg

---

## 直播高级设置
* 固定码率 & 变码率
* 分辨率 & 带宽消耗
* HLS延迟
* 服务端数据包缓冲大小设置
* 音视频同步

---

## 开发过程会遇到的问题
* rtmp协议的坑
* CPU占用
* 花屏 / 卡顿  - 缓冲区的控制
* 码流拷贝 - 内存占用与性能

---

## 问题

* 自动化测试, 集成测试, 测试结果可视化. 减少你测了没?
* 回源链 日志分析系统
* 数据分析系统 / 运维系统
* 测试机与线上机重复测试问题, 环境不同的问题, docker?

---

## Q&A

Thanks

Contribute your ideas!
