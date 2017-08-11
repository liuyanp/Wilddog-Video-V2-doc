title : 安装和初始化
--------------

本篇文档介绍如何安装 SDK 并初始化 WilddogVideo。

### 安装 SDK

- **使用 Maven 安装 Wilddog Video SDK**

<figure class="highlight xml"><table><tbody><tr><td class="code"><pre><div class="line"><span class="tag">&lt;<span class="name">dependency</span>&gt;</span></div><div class="line">    <span class="tag">&lt;<span class="name">groupId</span>&gt;</span>com.wilddog.client<span class="tag">&lt;/<span class="name">groupId</span>&gt;</span></div><div class="line">    <span class="tag">&lt;<span class="name">artifactId</span>&gt;</span>wilddog-video-android<span class="tag">&lt;/<span class="name">artifactId</span>&gt;</span></div><div class="line">    <span class="tag">&lt;<span class="name">version</span>&gt;</span><span class="media_android_v">1.0.0-beta</span><span class="tag">&lt;/<span class="name">version</span>&gt;</span></div>    <span class="tag">&lt;<span class="name">type</span>&gt;</span>aar<span class="tag">&lt;/<span class="name">type</span>&gt;</span></div><div class="line"><span class="tag">&lt;/<span class="name">dependency</span>&gt;</span></div></pre></td></tr></tbody></table></figure>


- **使用 Gradle 安装 Wilddog Video SDK**

<figure class="highlight java"><table><tbody><tr><td class="code"><pre><div class="line">dependencies { </div><div class="line">    compile <span class="string">&apos;com.wilddog.client:wilddog-video-android:<span class="media_android_v">1.0.0-beta</span>&apos;</span></div><div class="line">}</div></pre></td></tr></tbody></table></figure>

如果出现由于文件重复导致的编译错误，可以在 build.gradle 中添加 packingOptions:

```
android {
    ...
    packagingOptions {
        exclude 'META-INF/LICENSE'
        exclude 'META-INF/NOTICE'
    }
}
```

### 初始化 Video SDK

[WilddogVideo](/conversation/android/api/wilddog-video.html) 是 WilddogVideo SDK 功能的主入口。用户在使用 SDK 之前，要初始化 `WilddogVideo` 实例，以连接野狗服务器。

初始化之前，打开控制面板 - 应用 - 视频通话 - 配置，获取 VideoAppID。

初始化 `WilddogVideo` 之前，要先经过 [野狗身份认证](/auth/Android/index.html)。开发者可以根据需要选择匿名登录、邮箱密码、第三方或自定义认证等方式进行身份认证。

成功通过身份认证后，用户将获得 `uid` 以及 `token`。以匿名方式登录后初始化 [WilddogVideo](/conversation/android/api/wilddog-video.html) 为例：


```java
@Override
public void onCreate() {

    super.onCreate();

    //初始化WilddogApp实例,初始化WilddogApp后，即可在项目任意位置获取数据库地址引用
    //mAppId即野狗应用ID
    WilddogOptions.Builder builder = new WilddogOptions.Builder().setSyncUrl("http://"+ mAppId +".wilddogio.com");

    WilddogOptions options = builder.build();

    WilddogApp.initializeApp(getApplicationContext(), options);

    //获取Auth对象
    WilddogAuth auth = WilddogAuth.getInstance();

    //匿名登录系统
    auth.signInAnonymously().addOnCompleteListener(new OnCompleteListener<AuthResult>() {
        @Override
        public void onComplete(Task<AuthResult> task) {
            if (task.isSuccessful()) {
                //...
                //完成身份认证后初始化 Video SDK,如身份认证失败则会引起初始化失败或应用崩溃
                WilddogUser user = task.getResult().getCurrentUser();
                 initVideoSDK();

            }else {
                 throw  new RuntimeException("auth 失败"+task.getException().getMessage());
            }
        }
    });

    
    //....
}

private void initVideoSDK(){
    String token = WilddogAuth.getInstance().getCurrentUser().getToken(false).getResult().getToken();
    //初始化 WilddogVideo SDK
    WilddogVideo.initializeWilddogVideo(getApplicationContext(), mAppId,token);
    //获取 WilddogVideo对象
    WilddogVideo video＝WilddogVideo.getInstance();
}

```

### 代码混淆

在生成 apk 进行代码混淆时进行如下配置：

```
-keep class com.wilddog.client.**{*;} 
-keep class com.wilddog.**{*;} 

-keep class com.fasterxml.jackson.**{*;} 
-keep class com.fasterxml.jackson.databind.**{*;} 
-keep class com.fasterxml.jackson.core.**{*;} 
```

### 其余问题
在 Android Studio 进行 Sync Project 时会提示如下警告：
```
Warning:WARNING: Dependency org.json:json:20090211 is ignored for debug as it may be conflicting with the internal version provided by Android.
```

消除警告请进行如下配置，在模块级 build.gradle 文件的 android {} 中添加：

```
	configurations {
		compile.exclude group: "org.json", module: "json"
	}
```

### 设置代理

设置 [WilddogVideo](/conversation/android/api/wilddog-video.html) 的代理<[WilddogVideo.Listener](/conversation/iOS/api/wilddog-video-listener.html)> 用于监听通话请求：

```java
     video.setListener(new WilddogVideo.Listener() {
                @Override
                public void onCalled(Conversation conversation, String s) {
                    
                }
    
                @Override
                public void onTokenError(WilddogVideoError wilddogVideoError) {
    
                }
            });
```

实现代理方法 `onCalled(Conversation conversation, String s)`，当收到远端通话请求时，会触发该方法：

```java
     public void onCalled(Conversation conversation, String s) {
         // 处理通话请求。       
     }
```

实现代理方法 `-[WDGVideoDelegate wilddogVideo:didFailWithTokenError:]`，当 `token` 错误或过期时，会触发该方法：

```java
     public void onTokenError(WilddogVideoError wilddogVideoError) {
         // 处理 token 错误。
     }
```
