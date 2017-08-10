title: WDGConversationDelegate
---

[WDGConversation](url_placeholder) 的代理方法，用于通知 `WDGConversation` 发生的事件。

## 方法

### - conversation: didReceiveResponse:

**定义**

```objectivec
- (void)conversation:(WDGConversation *)conversation didReceiveResponse:(WDGCallStatus)callStatus;
```

**说明**

`WDGConversation` 通过调用该方法通知代理视频通话邀请的状态发生变化。

**参数**

 参数名 | 说明 
---|---
conversation | 调用该方法的 `WDGConversation` 实例。
callStatus   | 表示视频通话的状态，包括已接受、已拒绝、对方忙碌、请求超时。

</br>

---

### - conversation: didReceiveStream:

**定义**

```objectivec
- (void)conversation:(WDGConversation *)conversation didReceiveStream:(WDGRemoteStream *)remoteStream;
```

**说明**

`WDGConversation` 通过调用该方法通知代理收到远端媒体流。

**参数**

 参数名 | 说明 
---|---
conversation | 调用该方法的 `WDGConversation` 实例。
remoteStream | `WDGRemoteStream` 实例，表示对方传来的媒体流。

</br>

---

### - conversation: didFailedWithError:

**定义**

```objectivec
- (void)conversation:(WDGConversation *)conversation didFailedWithError:(NSError *)error;
```

**说明**

`WDGConversation` 通过调用该方法通知代理当前视频通话发生错误而未能建立连接。

**参数**

 参数名 | 说明 
---|---
conversation | 调用该方法的 `WDGConversation` 实例。
error | 错误信息，描述未能建立连接的原因。

</br>

---

### - conversationDidClosed:

**定义**

```objectivec
- (void)conversationDidClosed:(WDGConversation *)conversation;
```

**说明**

`WDGConversation` 通过调用该方法通知代理当前视频通话已被关闭。

**参数**

 参数名 | 说明 
---|---
conversation | 调用该方法的 `WDGConversation` 实例。

</br>

---
