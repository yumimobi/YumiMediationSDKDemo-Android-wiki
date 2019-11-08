## Initialization and request

```java
// Create a YumiMedia object.
//
// activity: Rewarded Video will displayed from the Activity
// YOUR_SLOT_ID: ad unit id or placement id, created with the YumiMediation platform
YumiMedia media = new YumiMedia(activity， "YOUR_SLOT_ID");

// Request a Rewarded Video, after the first call to this method, the ad will automatically request the next ad after the closure or request failure
media.requestYumiMedia();
```

## Display and Destroy

show Rewarded Video
```java
media.showMedia();
```

Destroy reward video object: Call the `destroy()` method only when you don't need to show reward video ads. It is recommended to call this method in the Activity `onDestroy()` life callback.

```java
media.destroy()
```

## Add Listener

If you need to listen to the Rewarded Video method callback, after creating the YumiMedia object, call the following method

```java
media.setMediaEventListener(iYumiMediaListener);
```

the IYumiMediaListener interface is defined as follows:

```java
interface IYumiMediaListener {
    // This method is fired when Rewarded Video is loaded.
    void onMediaPrepared();
    // This method is fired when the Rewarded Video fails to load. Print adError to view the error details.
    void onMediaPreparedFailed(AdError adError);
    // This method is fired when Rewarded Video is displayed to the screen.
    void onMediaExposure();
    // This method is fired when Rewarded Video does not successfully display the ad after calling the display method. Print adError to view the error details.
    void onMediaExposureFailed(AdError adError);
    // This method is fired when an ad is clicked
    void onMediaClicked();
    // This method is fired when Rewarded Video is closed. isRewarded indicates whether the reward should be issued. For example, if you choose to skip the advertisement during playback, this close event will also be fired. At this time, isRewarded is false, indicating that the reward should not be issued.
    void onMediaClosed(boolean isRewarded);
    // Rewarded Video rewarded callback, you should issue a reward at this time (this method as same as onMediaClosed (true) , to avoid repeating the award)
    void onMediaRewarded();
    // This method is fired when the video starts playing
    void onMediaStartPlaying();
}
```

## Other methods
```java
// Determine if there is a ready advertisement
media.isReady();
// Returns the remaining number of reward ads. If it is 0, it means that Rewarded Video will not be requested again today.
media.getMediaRemainRewards()
```

<div style="background-color:rgb(228,244,253);padding:10px;">
<span style="color:rgb(62,113,167);">
<b>Note:</b> Do not call the isReady() method frequently, it is recommended to call the interval for no less than 5 seconds.
</span>
</div>