# Import the Yumi SDK
## Android Studio

add YumiMediationSDK and other network adapters maven url to project's build.gradle

```groovy
buildscript {
    repositories {
        jcenter()
    }
}

allprojets {
    repositories {
    	jcenter()

        // Optional. It is required when you import SDKs related to Google Server.
        google()
        
        // Optional.
        // If you do not need the Innerative and bytedance SDK, you can remove the repo.
        maven { url "https://dl.bintray.com/yumimobi/thirdparty/" }
        maven { url "https://dl.bintray.com/yumimobi/ads/" }

        // Optional.
        // If you do not need the tapjoy SDK, you can remove the repo.
        maven { url "https://tapjoy.bintray.com/maven" }

        // Optional.
        // If you do not need the pubnative SDK, you can remove the repo.
        maven { url "https://dl.bintray.com/pubnative/maven" }
        
    }
}
```

add YumiMediationSDK and other adapters dependencies.

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

> Platform adapter, [Click here](https://github.com/yumimobi/YumiMediationSDKDemo-Android-wiki/blob/master/docs/YumiMediationSDK%20-%20Mediation%20List(en)%20.md) 

Optional permission.

```xml
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.MOUNT_UNMOUNT_FILESYSTEMS"/>
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
<uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION" />
<!-- The Googleplay app can be unloaded -->
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<!-- If no add READ_PHONE_STATE permission will affect the advertising earnings -->
<uses-permission android:name="android.permission.READ_PHONE_STATE"/>
```

## Eclipse

Add library file to libs.

>[SDK Download](https://github.com/yumimobi/YumiMediationSDKDemo-Android-wiki/blob/master/docs/YumiMediationSDK%20for%20Android%20Download%20Page.md)

All lib files are placed in ..\YumiMobi_SDK_AndroidEclipse_Example\lib in the SDK:

- YumiMobi_Android_vX.X.X.jar

- android-support-v4.jar

- android-support-v7-appcompat.jar

- google_play_service 

Create libs folder under the root directory of your project,add YumiMobi_Android_vX.X.X.jar into libs.

<img src="https://github.com/yumimobi/YumiMediationSDKDemo-Android-wiki/blob/master/docs/document/image01.jpg" alt="img1">

you can choose to or not to add android-support-v4.jar and/or android-support-v7-appcompat.jar into libs according to your needs. You must use the jar file provided by YUMIMOBI when you need to use v4.jar or v7.jar.

<div style="background-color:rgb(228,244,253);padding:10px;">
<span style="color:rgb(62,113,167);">About google_play_service project: google_play_service is not mandatory, while some ad platforms need it. YUMIMOBI does not need google_play_service. You need use it as a library and import it into your project. Also, add the ollowing code in tab <application> of your manifest.xml.</span></div>
<br/>

```xml
<meta-data 
    android:name="com.google.android.gms.version"
    class="kix-line-break"
    android:value="@integer/google_play_services_version" />
```

Registered components

Add following in manifest.xml of your project:

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

Add permissions 

- Add the following permissions in manifest.xml of your project:

```xml
<uses-permission android:name="android.permission.INTERNET"/>
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<!--The Googleplay app can be unloaded-->
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
```

- Optional permission

```xml
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.MOUNT_UNMOUNT_FILESYSTEMS"/>
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
<uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION" />

<!-- If no add READ_PHONE_STATE permission will affect the advertising revenue -->
<uses-permission android:name="android.permission.READ_PHONE_STATE"/>
```

## Proguard
If your project turn on minifyEnabled, add the following to the proguard file.

```c
-keepattributes Exceptions,InnerClasses,Signature,Deprecated,SourceFile,LineNumberTable,*Annotation*,Synthetic,EnclosingMethod
-keep class com.yumi.android.sdk.ads.** { *;}
-keep class com.playableads.**{*;}
```
<b>Important：</b>If you integrated three-party advertising platforms, please set up a three-party platform Proguard configuration according to the three-party platform documentation we provide.[Click here](https://github.com/yumimobi/YumiMediationSDKDemo-Android-wiki/blob/master/docs/YumiMediationSDK%20-%20Mediation%20List(en)%20.md) 


[GetDemo](https://github.com/yumimobi/YumiMediationSDKDemo-Android)