title: 媒体流
---

本篇文档介绍如何创建、配置和播放媒体流（包括摄像头采集的视频流和麦克风采集的音频流以及接收到的远端媒体流）。

WilddogRoom 中使用 Stream 的概念来表示视频通话的参与者。每个参与者将自己的本地媒体流上传到服务器，同时从服务器获得其他参与者的媒体流。

在视频会议中，Stream 只包含了简单的流的描述信息，要获取到多媒体数据，需要订阅该媒体流。详情请阅读 [发布和订阅](placeholder)。

## 本地媒体流 (LocalStream)

### 1. 创建本地媒体流

本地媒体流包含了本地设备所采集的音频、视频信息，是视频会议所需要的基本数据。在加入视频会议之前，需要创建 [WDGLocalStream](placeholder) 实例：

```objectivec
WDGLocalStream *localStream = [[WDGLocalStream alloc] initWithOptions:options];
```

### 2. 配置本地媒体流

创建本地媒体流需传入 [WDGLocalStreamOptions](placeholder) 对象，用于确定本地视频流的音频、视频开关、最大尺寸和最大帧率：
* shouldCaptureAudio / shouldCaptureVideo 为音／视频采集的开关，设置为 NO 表示关闭音／视频采集，默认为 YES；
* dimension 用来设置视频的最大尺寸，默认为 480p，如果网络条件较差，会自动降低尺寸大小；
* maxFPS 用来设置视频的最大帧率，默认为 16 帧／秒，如果网络条件较差，会自动降低帧率。

```objectivec
WDGLocalStreamOptions *localStreamOption = [[WDGLocalStreamOptions alloc] init];
localStreamOption.shouldCaptureAudio = YES;
localStreamOption.shouldCaptureVideo = YES;
localStreamOptions.dimension = WDGVideoDimensions720p;
localStreamOptions.maxFPS = 20;
```

### 3. 播放本地媒体流

本地媒体流包括音频和视频。默认不播放音频，使用 [WDGVideoView](placeholder) 播放视频。

播放本地视频流：

```objectivec
[localStream attach:self.localVideoView];
```

停止播放本地视频流：

```objectivec
[localStream detach:self.localVideoView];
```

可以设定 `audioEnabled` 和 `videoEnabled` 两个方法来控制是否播放音频、视频，默认都为开启。

> BUG: 本地音频播放不开启？

```objectivec
// 设置不播放媒体流的视频
localStream.videoEnabled = YES;
```

## 远端媒体流 (RemoteStream)

```c
// 远端媒体流需要从服务器获取。在视频会议中，远端媒体流有 MCU 和 SFU 两种模式。在 MCU 模式下，服务器会将收到的所有远端媒体流进行混流处理，并作为一个媒体流发给客户端。在 SFU 模式下，服务器将远端媒体流转发给客户端，客户端可能收到多个独立的媒体流。
```

### 1. 获取远端媒体流

通过 `-[WDGRoomDelegate wilddogRoom:didStreamAdded:]` 回调方法获取远端媒体流。

### 2. 播放远端媒体流

远端媒体流包括音频和视频。默认播放音频，使用 [WDGVideoView](placeholder) 播放视频。

播放本地视频流：

```objectivec
[remoteStream attach:self.remoteVideoView];
```

停止播放本地视频流：

```objectivec
[remoteStream detach:self.remoteVideoView];
```

可以设定 `audioEnabled` 和 `videoEnabled` 两个方法来控制是否播放音频、视频，默认都为开启。

```objectivec
// 设置不播放媒体流的视频
remoteStream.videoEnabled = YES;
```
