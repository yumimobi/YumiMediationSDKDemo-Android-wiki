## 初始化及请求
```java
// 创建 YumiBanner 对象
//
// activity: 展示横幅广告的 Activity
// YOUR_SLOT_ID: 通过玉米移动平台创建的广告位 ID
// auto: 是否自动加载下一条广告
//  - true 横幅广告加载失败或展示一定时间后，自动请求并展示下一条横幅广告
//  - false 不自动加载下一条广告，需要再次调用 requestYumiBanner() 方法才能显示下一条。
YumiBanner banner = new YumiBanner(activity， "YOUR_SLOT_ID"， auto);

// 必需调用 setBannerContainer 方法将广告必需的信息传给 SDK，否则不会有广告展示
// 
// bannerContainer: 广告容器（ViewGroup），广告内容会填充到此容器中。SDK 会根据屏幕大小调整传入的容器尺寸，比如，传入的容器宽度超出屏幕宽度后，会自动缩小容器宽度并相应调整容器的高度
// AdSize: 广告样式，SDK 会根据广告样式调整容器尺寸，有以下 4 种，
//  - BANNER_SIZE_AUTO：SDK 根据屏幕大小调整容器大小，如果检测到设备是手机，则设置容器大小为 320*50；如果设备是平板，则设置容器大小为 728*90
//  - BANNER_SIZE_SMART：目前三方 Network 中只有 AdMob 支持 SMART 广告，其它 Network 会直接返回无广告。具体详情请参考 AdMob SMART_BANNER
//  - BANNER_SIZE_320X50：SDK 将容器设置为 320*50 大小
//  - BANNER_SIZE_728X90：SDK 将窗口设置为 728*90 大小
// isMatchWindowWidth: true 代表将容器扩展到与屏幕等宽（仅在竖屏有效），高度与宽度比为 1:8(BANNER_SIZE_728X90) 或 1:6.4(非 BANNER_SIZE_728X90)
banner.setBannerContainer(bannerContainer, AdSize.BANNER_SIZE_AUTO, isMatchWindowWidth);

// 请求横幅广告，如果 auto 属性设置为 true，则只需要调用一次该方法即可
banner.requestYumiBanner();
```

## 销毁广告

```java
banner.destroy();
```

当不再需要展示横幅广告时销毁 banner 对象，建议在 Activity `onDestroy()` 回调方法中销毁。如果只是想暂时隐藏 Banner 广告，可以调用 `dismissBanner()` 方法，在需要再次展示时调用 `resumeBanner()` 方法来重新显示广告。

## 监听事件

如果需要监听横幅广告方法回调，请在创建 YumiBanner 对象后，调用如下方法

```java
banner.setBannerEventListener(iYumiBannerListener);
```

IYumiBannerListener 接口定义如下

```java
interface IYumiBannerListener {
    // 广告加载完毕时触发此方法
    void onBannerPrepared();
    // 广告加载失败时触发此方法，打印 adError 查看错误详情
    void onBannerPreparedFailed(AdError adError);
    // 广告展示到屏幕上时触发此方法
    void onBannerExposure();
    // 点击广告时触发此方法
    void onBannerClicked();
    // 关闭广告时会触发此方法，调用 dismissBanner() 方法不会触发此方法
    void onBannerClosed();
};
```

## 其它方法
```java
// 隐藏横幅，同时暂停横幅轮换请求
banner.dismissBanner();
// 恢复显示横幅，同时恢复横幅轮换请求
banner.resumeBanner();
```