title: WilddogVideoView
---

视频流展示控件。
## 方法

### setMirror(boolean)

**定义**   

```java
public void setMirror(boolean mirror)
```

**说明**

设置当前媒体流展示控件是否以镜像方式展示媒体流（视频流），默认不镜像展示。

**参数**

| 参数名 | 描述 |
|---|---|
|mirror|设置当前的 `WilddogVideoView` 是否以镜像方式展示画面，本地媒体流展示控件通常设置为 true ，默认不镜像展示。 |

**示例**

```java
        local_video_view.setMirror(true);
```

</br>

---

### setVideoScaleType(ScalingType)

**定义**   

```java
void setVideoScaleType(ScalingType videoScaleType)
```

**说明**

设置当前媒体流展示控件的媒体流的缩放展示方式。

**参数**

| 参数名 | 描述 |
|---|---|
|videoScaleType|[ScalingType](conversation/Android/api/scaling-type.html),默认为`SCALE_ASPECT_FIT`。 |

</br>

---

### release()

**定义**   

```java
public void release()
```

**说明**

释放当前视频展示控件。在关闭页面时需要调用此方法释放视频展示控件。


</br>
