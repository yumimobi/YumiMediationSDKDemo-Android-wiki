## Initialization and request
```java
// Creates a YumiBanner object
//
// activity: your banner view will add to the activity.
// YOUR_SLOT_ID: ad unit id or placement id, created with the YumiMediation platform
// auto: Whether to automatically load the next ad
//  - true: Automatically request and display the next banner after the banner has failed to load or show for a certain amount of time
//  - false: Do not automatically load the next ad, you need to call the requestYumiBanner() method again to display the next one.
YumiBanner banner = new YumiBanner(activity， "YOUR_SLOT_ID"， auto);

// Must pass the base information by the setBannerContainer method to the SDK, otherwise there will be no ad to load.
// 
// bannerContainer: ad coantiner(ViewGroup), Ad content will be filled in this container. The SDK will adjust the size of the incoming container according to the screen size. For example, if the width of the incoming container exceeds the width of the screen, it will automatically reduce the width of the container and adjust the height of the container accordingly.
// AdSize: Banner style. The SDK will adjust the container size according to the style, there are 4 styles, as followed
//  - BANNER_SIZE_AUTO：The SDK resizes the container according to the screen size. If it detects that the device is a mobile phone, set the container size to 320 * 50; if the device is a tablet, set the container size to 728 * 90
//  - BANNER_SIZE_SMART：Currently, only AdMob supports SMART Banner in the three-party network, and other networks directly return no ads. Please refer to AdMob SMART_BANNER for details.
//  - BANNER_SIZE_320X50：The SDK sets the container to 320*50 size
//  - BANNER_SIZE_728X90：The SDK sets the container to 728*90 size
// isMatchWindowWidth: True means that the container is expanded to the same width as the screen (valid only in portrait), with a height to width ratio of 1:8 (BANNER_SIZE_728X90) or 1:6.4 (non-BANNER_SIZE_728X90)
banner.setBannerContainer(bannerContainer, AdSize.BANNER_SIZE_AUTO, isMatchWindowWidth);

// Request a banner ad, if the auto property is set to true, then you only need to call this method once.
banner.requestYumiBanner();
```

## Destroy

```java
banner.destroy();
```

Deleting the banner object when it is no longer necessary to display , the banner is recommended to be destroyed in the Activity `onDestroy()` life callback. If you just want to temporarily hide the Banner ad, you can call the `dismissBanner()` method and call the `resumeBanner()` method to redisplay the ad when it needs to be displayed again.

## Add Listener

If you need to listen for banner ad method callbacks, after creating the YumiBanner object, call the following method

```java
banner.setBannerEventListener(iYumiBannerListener);
```

The IYumiBannerListener interface is defined as follows

```java
interface IYumiBannerListener {
    // This method is fired when the ad is loaded
    void onBannerPrepared();
    // This method is fired when the ad fails to load, print adError to view the error details
    void onBannerPreparedFailed(AdError adError);
    // This method is fired when the ad is displayed on the screen
    void onBannerExposure();
    // This method is fired when an ad is clicked
    void onBannerClicked();
    // This method is fired when the ad is closed, and calling the dismissBanner() method does not trigger this method.
    void onBannerClosed();
}
```

## Other methods
```java
// hide banner
banner.dismissBanner();
// Restore display banner
banner.resumeBanner();
```