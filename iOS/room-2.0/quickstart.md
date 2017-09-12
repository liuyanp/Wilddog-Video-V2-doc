title: 快速入门
---
我们通过一个简单的 4 人视频会议示例来说明 Video SDK 的用法。[下载快速入门](https://github.com/WildDogTeam/video-demo-ios-conference/archive/master.zip)

<div class="env">
    <p class="env-title">环境准备</p>
    <ul>
        <li> Xcode 7.0 及以上版本 </li>
        <li> iOS 8.0 及以上版本 </li>
    </ul>
</div>


## 1. 创建应用

首先，在控制面板中创建应用。

<img src='/images/video_quickstart_create.png' alt="video_quickstart_create">

## 2. 开启匿名登录

应用创建成功后，进入 管理应用-身份认证-登录方式，开启匿名登录。

<img src='/images/openanonymous.png' alt="video_quickstart_openanonymous">

## 3. 开启实时视频通话

进入 管理应用-实时视频通话，开启视频通话功能。此处注意记下配置页面的`VideoAppID`

<img src='/images/video_quickstart_openVideo.png' alt="video_quickstart_openVideo">

## 4. 安装快速入门

使用 Cocoapods 管理快速入门包。进入工程目录，执行以下命令，自动下载依赖并更新到最新版。

```shell
 $ pod install
 $ pod setup
 $ pod update
```

下载完毕后会自动创建 `WilddogRoomDemo.xcworkspace` ，打开：

```shell
 $ open WilddogRoomDemo.xcworkspace
```

在 Xcode 中编译运行视频会议示例，把快速入门安装到 iPhone 中。


## 5. 运行快速入门

连接 iPhone，运行快速入门。

## 6. 登录快速入门

快速入门运行成功后，输入`VideoAppID`。

<img src='/images/video_quickstart_ios_conference_0.jpg' alt="video_quickstart_ios_mainUI" width="300">

`VideoAppID`为下图所示，然后点击匿名登录。

<img src='/images/video_quickstart_videoappid.png' alt="video_quickstart_videoappid">

登录成功后，输入会议 ID。会议 ID 可以是别人创建后提供的 ID ，如果当前没有会议，可自己创建一个会议 ID 。

<img src='/images/video_quickstart_ios_conference_1.jpg' alt="video_quickstart_android_conference_join" width="300" >

加入会议后，页面会显示本地视频画面、你的会议 ID 和操作按钮。

<img src='/images/video_quickstart_ios_conference_2.jpg' alt="video_quickstart_android_conference_mainUI" width="300" >

## 7. 其他人加入会议

重复上述步骤，在其他手机端登录后，输入同一会议 ID， 加入会议。

<img src='/images/video_quickstart_ios_conference_3.jpg' alt="video_quickstart_android_conference_multi" width="300" >


更多详细功能请见 [完整指南](placeholder)。
