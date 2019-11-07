# Splash

## Initialization and request

```java
// Create a YumiSplash object
// 
// activity: The splash ad will appear in the adContainer container of this activity
// adContainer: Splash ad container (ViewGroup, it is recommended to use FrameLayout as the ad container), the ad will be displayed in this container
// YOUR_SLOT_ID: ad unit id or placement id, created with the YumiMediation platform
YumiSplash splash = new YumiSplash(activity, adContainer, "YOUR_SLOT_ID");

// Request and display an splash ad
splash.loadAdAndShowInWindow();
```

## Add Listener

To monitor the splash ad method callback, after creating the YumiSplash object, call the following method

```java
splash.setSplashListener(iYumiSplashListener);
```

The IYumiSplashListener interface is defined as follows

```java
interface IYumiSplashListener {
    // This method is fired when the ad is successful
    void onSplashAdSuccessToShow();
    // This method is fired when the ad fails to display successfully, print adError to view the error details
    void onSplashAdFailToShow(AdError adError);
    // This method is fired when clicking to open the screen
    void onSplashAdClicked();
    // This method is fired when the ad is closed
    void onSplashAdClosed();
}
```

## Other methods
```java
// Set the launch image to display this image during the loading of the splash ad
splash.setLaunchImage(drawable);
// Set the length of the request ad. The default is 3 seconds. If it is not loaded within 3 seconds, it will fired the failure callback directly. Here, 3 seconds is the approximate number.
splash.setFetchTime(seconds);
```