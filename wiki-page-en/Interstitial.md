# Interstitial

## Initialization and request

```java
// Create a YumiInterstitial object.
// 
// activity: Interstitial will appear in this activity
// YOUR_SLOT_ID: ad unit id or placement id, created with the YumiMediation platform
// auto: Whether to automatically load the next ad
//  - true: When the displaying ad ends or the ad fails to load, the SDK will automatically request the next ad at the appropriate time.
//  - false: When the ad has been displayed, the ad will not be automatically requested.
YumiInterstitial interstitial = new YumiInterstitial(activity， "YOUR_SLOT_ID"， auto);

// Request an ad, if the auto property is set to true, then you only need to call this method once.
interstitial.requestYumiInterstitial();
```

<div style="background-color:rgb(228,244,253);padding:10px;">
<span style="color:rgb(62,113,167);">
<b>Important:</b> When showing the ad, you must use the interstitial.onBackPressed() method to avoid the back key logic confusion. For example, when there is an ad being displayed, clicking the back button should close the ad instead of closing the current activity. Sample code is as follows
</span>
</div>
<br/>

```java
@Override
public void onBackPressed() {
    if (interstitial.onBackPressed()) {
        return;
    }
    super.onBackPressed();
}
```

## Display and Destroy

```java
// Display ad
interstitial.showInterstitial();
```

```java
// Destroy the ad instance
interstitial.destroy();
```

Calling the `destroy()` method only when you don't need to display the ad, it is recommended to call this method in the Activity `onDestroy()` life callback.

## Add Listener

If you need to listen to the ad method callback, after creating the YumiInterstitial object, call the following method

```java
interstitial.setInterstitialEventListener(iYumiInterstitialListener);
```

the IYumiInterstitialListener interface is defined as follows
```java
interface IYumiInterstitialListener {
    // This method is fired when the ad is loaded.
    void onInterstitialPrepared();
    // This method is fired when the ad fails to load, print adError to view the error details
    void onInterstitialPreparedFailed(AdError adError);
    // This method is fired when an ad appears on the screen
    void onInterstitialExposure();
    // This method is fired when an ad is clicked
    void onInterstitialClicked();
    // This method is fired when closing the ad
    void onInterstitialClosed();
    // This method is fired when the showInterstitial() method is called and failed to show an ad, print adError to view the error details
    void onInterstitialExposureFailed(AdError adError);
    // This method is fired when the video starts playing when the video is inserted in the ad. If there is no video in the screen, the method is fired after the advertisement is displayed.
    void onInterstitialStartPlaying();
}
```

## Other methods
```java
// Determine if an ad is available
interstitial.isReady();
```