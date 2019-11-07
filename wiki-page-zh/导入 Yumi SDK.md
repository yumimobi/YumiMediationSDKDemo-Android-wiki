# 导入 Yumi SDK
## Android Studio 接入

配置聚合主包及各 Network

在项目根目录下的 build.gradle 文件中添加以下配置

```groovy
buildscript {
    repositories {
        jcenter()
    }
}

allprojets {
    repositories {
    	jcenter()

        // 可选，如果需要导入 Google Server 相关的 SDK 时需要添加以下 repo
        google()
        
        // 可选，如果需要导入 Innerative，bytedance 相关的 SDK 时需要添加以下 repo
        maven { url "https://dl.bintray.com/yumimobi/thirdparty/" }
        maven { url "https://dl.bintray.com/yumimobi/ads/" }

        // 可选，如果需要导入 Tapjoy 相关 SDK 时需要添加以下 repo
        maven { url "https://tapjoy.bintray.com/maven" }

        // 可选，如果需要导入 Pubnative 相关 SDK 时需要添加以下 repo
        maven { url "https://dl.bintray.com/pubnative/maven" }
    }
}
```

在 app 下的 build.gradle 中添加依赖相关依赖

```groovy
dependencies {
    // YumiMediationSDK main package
    implementation 'com.yumimobi.ads:mediation:4.3.0'

    // YumiMediationSDK adapters, each adapter is one third party sdk.
    implementation 'com.yumimobi.ads.mediation:playableads:4.3.0'
    implementation 'com.yumimobi.ads.mediation:adcolony:4.3.0'
    implementation 'com.yumimobi.ads.mediation:admob:4.3.0'
    implementation 'com.yumimobi.ads.mediation:applovin:4.3.0'
    implementation 'com.yumimobi.ads.mediation:baidu:4.3.0'
    implementation 'com.yumimobi.ads.mediation:bytedance:4.3.0'
    implementation 'com.yumimobi.ads.mediation:chartboost:4.3.0'
    implementation 'com.yumimobi.ads.mediation:facebook:4.3.0'
    implementation 'com.yumimobi.ads.mediation:gdt:4.3.0'
    implementation 'com.yumimobi.ads.mediation:inmobi:4.3.0'
    implementation 'com.yumimobi.ads.mediation:inneractive:4.3.0'
    implementation 'com.yumimobi.ads.mediation:ironsource:4.3.0'
    implementation 'com.yumimobi.ads.mediation:ksyun:4.3.0'
    implementation 'com.yumimobi.ads.mediation:mintegral:4.3.0'
    // If you publish an app in China, you can use mintegral-china sdk
    // compile 'com.yumimobi.ads.mediation:mintegral-china:4.3.0'
    implementation 'com.yumimobi.ads.mediation:oneway:4.3.0'
    implementation 'com.yumimobi.ads.mediation:tapjoy:4.3.0'
    implementation 'com.yumimobi.ads.mediation:unity:4.3.0'
    implementation 'com.yumimobi.ads.mediation:vungle:4.3.0'
    implementation 'com.yumimobi.ads.mediation:pubnative:4.3.0'
｝
```

> 最新版本号，请[查看](https://github.com/yumimobi/YumiMediationSDKDemo-Android#latest-version)

> 聚合平台Adapter详细说明，请[查看](./YumiMediationSDK%20-%20Mediation%20List(zh-cn)%20.md)

添加可选权限，可选权限可以提升广告填充率及广告转化效果。

```xml
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.MOUNT_UNMOUNT_FILESYSTEMS"/>
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
<uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION" />
<!--此权限受 Android 系统限制，若无此权限可能导致部分机型对下载类广告无法直接下载，国内渠道必须添加，Googleplay（一般为直接跳转型广告）可不加-->
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<!--此权限受 Android 系统限制，请添加，如果不添加将影响广告收益-->
<uses-permission android:name="android.permission.READ_PHONE_STATE"/>
```

 ## Eclipse 接入

**第一步：下载并添加聚合SDK：**

>[SDK 下载列表](https://github.com/yumimobi/YumiMediationSDKDemo-Android/blob/master/docs/YumiMediationSDK%20for%20Android%20Download%20Page.md)

玉米移动广告需要的lib文件均放在 ..\YumiMobi_SDK_AndroidEclipse_Example\lib 文件夹下：

- YumiMobi_Android_vX.X.X.jar

- android-support-v4.jar

- android-support-v7-appcompat.jar

- google_play_service的lib工程

使用时在工程的根目录下创建 libs 文件夹，将 YumiMobi_Android_vX.X.X.jar 添加到创建好的 libs 文件中。

<img src="document\image01.jpg" alt="img1">

可以视需求添加 android-support-v4.jar、android-support-v7-appcompat.jar 到 libs 文件中，需要用到 V4 或 V7 包时必须使用我们提供的 jar。

<div style="background-color:rgb(228,244,253);padding:10px;">
<span style="color:rgb(62,113,167);">关于 google_play_service 工程：
google_play_service 工程非必加，部分平台广告需要 google_play_service 支持，玉米移动广告不需要添加。使用时需要将此工程作为 library 工程，添加到您的工程中。并在 manifest.xml 文件的 &lt;application&gt; 
标签内增加以下代码：</span></div>
<br/>

```xml
<meta-data 
    android:name="com.google.android.gms.version"
    class="kix-line-break"
    android:value="@integer/google_play_services_version" />
```

**第二步：注册组件**

如以jar包方式接入SDK，请在工程中的manifest.xml文件中添加：

```xml
    <receiver android:name="com.yumi.android.sdk.ads.self.module.receiver.ADReceiver">
        <intent-filter>
            <action android:name="android.intent.action.DOWNLOAD_COMPLETE" />
        </intent-filter>
    </receiver>

    <activity
        android:name="com.yumi.android.sdk.ads.self.activity.YumiFullScreenActivity"
        android:configChanges="keyboardHidden|orientation|screenSize"
        android:theme="@android:style/Theme.NoTitleBar.Fullscreen" />

    <activity
        android:name="com.playableads.presenter.APIAdActivity"
        android:configChanges="keyboardHidden|orientation|screenSize"
        android:theme="@android:style/Theme.NoTitleBar.Fullscreen" />

    <activity
        android:name="com.playableads.presenter.PlayableADActivity"
        android:configChanges="orientation|screenSize|keyboardHidden"
        android:hardwareAccelerated="true"
        android:screenOrientation="portrait"
        android:theme="@android:style/Theme.NoTitleBar.Fullscreen" />

    <activity
        android:name="com.playableads.presenter.NativeAdLandingPageActivity"
        android:configChanges="orientation|screenSize|keyboardHidden"
        android:hardwareAccelerated="true"
        android:screenOrientation="portrait"
        android:theme="@android:style/Theme.NoTitleBar.Fullscreen" />

    <activity
        android:name="com.playableads.presenter.WebActivity"
        android:configChanges="orientation|screenSize|keyboardHidden"
        android:hardwareAccelerated="true"
        android:theme="@android:style/Theme.NoTitleBar.Fullscreen" />

    <receiver android:name="com.playableads.PlayableReceiver">
        <intent-filter>
            <action android:name="android.intent.action.DOWNLOAD_COMPLETE" />
        </intent-filter>
    </receiver>
        
    <activity android:name="com.yumi.android.sdk.ads.mediation.activity.MediationTestActivity" />
```

**第三步：添加权限**

- 如以jar包方式接入SDK，请在工程中的manifest.xml中添加以下权限

```xml
<uses-permission android:name="android.permission.INTERNET"/>
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<!--此权限受 Android 系统限制，若无此权限可能导致部分机型对下载类广告无法直接下载，国内渠道必须添加，Googleplay（一般为直接跳转型广告）可不加-->
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
```

- 可选权限


```xml
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.MOUNT_UNMOUNT_FILESYSTEMS"/>
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
<uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION" />

<!--此权限受 Android 系统限制，请添加，如果不添加将影响广告收益-->
<uses-permission android:name="android.permission.READ_PHONE_STATE"/>
```

## Proguard
如果您的工程需要混淆编译， 请在混淆文件内增加以下内容。

```java
-keepattributes Exceptions,InnerClasses,Signature,Deprecated,SourceFile,LineNumberTable,*Annotation*,Synthetic,EnclosingMethod
-keep class com.yumi.android.sdk.ads.** { *;}
-keep class com.playableads.**{*;}
```

<b>重要提示：</b>如果你有接入其他广告平台，请根据我们提供的三方平台文档设置三方平台混淆配置，请[查看](./YumiMediationSDK%20-%20Mediation%20List(zh-cn)%20.md)。