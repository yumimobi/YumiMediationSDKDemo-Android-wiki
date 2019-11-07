# Native

## Initialization and request
```java
// Create a native ad option for custom style. The following is the default style. Details are discussed in latter.
YumiNativeAdOptions nativeAdOptions = new YumiNativeAdOptions.Builder().build();

// Create a YumiNative object
//
// activity: 
// YOUR_SLOT_ID: ad unit id or placement id, created with the YumiMediation platform
// nativeAdOptions: style config object
YumiNative nativeAd = new YumiNative(activity, "YOUR_SLOT_ID", nativeAdOptions);

// load ad
// 
// adCount: The number of native ads loaded this time
nativeAd.requestYumiNative(adCount); 
```

## Add litener
To listen to the native ad callback method, after creating the YumiNative object, call the following method
```java
nativeAd.setNativeEventListener(iYumiNativeListener);
```

The IYumiNativeListener interface is defined as follows
```java
interface IYumiNativeListener {
    // This method is fired when the native ad is loaded
    void onLayerPrepared(List<NativeContent> adList);
    // This method is fired when the native ad fails to load, print adError to view the error details
    void onLayerFailed(AdError adError);
    // This method is fired when a native ad is clicked
    void onLayerClick();
    // This method is fired when a ExpressAdView render failed(only gdt ExpressAdView could callback it).
    void onExpressAdRenderFail(NativeContent content, String errorMsg);
    // This method is fired when ExpressAdView render success(only gdt ExpressAdView could callback it).
    void onExpressAdRenderSuccess(NativeContent content);
    // This method is fired when ExpressAdView closed(only gdt ExpressAdView could callback it).
    void onExpressAdClosed(NativeContent content);
}
```

## Display ad

* YumiNativeAdView class：

For the YumiNativeAdView format, there is the corresponding YumiNativeAdView class. This class is a ViewGroup that publishers should use as the root for the YumiNativeAdView. A single YumiNativeAdView corresponds to a single unified native ad. Each view used to display that ad's assets should be a child of the YumiNativeAdView object.

1、The view hierarchy for a unified native ad that uses a LinearLayout to display its asset views might look like this：

```xml
<?xml version="1.0" encoding="utf-8"?>
<com.yumi.android.sdk.ads.formats.YumiNativeAdView xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="wrap_content">
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:layout_gravity="center"
    android:background="#FFFFFF"
    android:minHeight="50dp"
    android:orientation="vertical">
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="vertical"
        android:paddingLeft="20dp"
        android:paddingRight="20dp"
        android:paddingTop="12dp">
        <LinearLayout
            android:orientation="horizontal"
            ...>
            <ImageView
                android:id="@+id/app_icon"
                .../>
            <LinearLayout
                android:orientation="vertical"
                ...>
                <TextView
                    android:id="@+id/headline"
                    .../>
                <RatingBar
                    android:id="@+id/stars"
                     .../>
            </LinearLayout>
        </LinearLayout>
        // Other assets such as image or media view, call to action, etc follow.
        ...
    </LinearLayout>
</LinearLayout>
</com.yumi.android.sdk.ads.formats.YumiNativeAdView>
```
2、Here is an example code snippet that creates a YumiNativeAdView and populates it with a NativeContent：

```java
private void showNativeAd() {
    // determine if the ad returned by the native callback onLayerPrepared() interface is empty
    if (adContentList != null && adContentList.size() > 0) {
        NativeContent content = adContentList.get(0);// git one native ad
        // determine this Native Ad is expired，true :  expired；false ：not expired.
        // if expired，please not show this Native Ad, request new Native Ad
        if(content.isExpired()){
            return;
        }

        // creater native ad Continer view，use to show Native ad
        FrameLayout nativeAdContinerView = (FrameLayout) findViewById(R.id.ll_ad_continer);
        // To detect current content is or not an ExpressAdView
        if (content.isExpressAdView()) {
            // If current content is an ExpressAdView, you should get the View by content.getExpressAdView() and then add the 
            // view into ad container
            YumiNativeAdView adView = (YumiNativeAdView) getLayoutInflater().inflate(R.layout.activity_native_material, null);
            adView.removeAllViews();

            FrameLayout.LayoutParams videoViewLayout = new FrameLayout.LayoutParams(WRAP_CONTENT, WRAP_CONTENT);
            videoViewLayout.gravity = Gravity.CENTER;

            adView.addView(content.getExpressAdView(), videoViewLayout);
            adView.setNativeAd(content);
            nativeAdContinerView.setClickable(true);
            nativeAdContinerView.addView(adView);
        } else {
            // Assumes that your ad layout is in a file call activity_native_material.xml
            // in the res/layout folder
            YumiNativeAdView adView = (YumiNativeAdView) getLayoutInflater().inflate(R.layout.activity_native_material, null);

            // Locate the view that will hold the title, set its text, and call the YumiNativeAdView's setTitleViewmethod to register it.
            adView.setTitleView((TextView) adView.findViewById(R.id.headline));

            ...
            // Repeat the above process for the other assets in the YumiNativeAdView using additional view objects (Buttons, ImageViews, etc).
            ...

            // If you want to display a video ad, please register the container（FrameLayout）that displays the video  
            adView.setMediaLayout((FrameLayout) adView.findViewById(R.id.media_content));


            // fill the title view using the string asset provided by NativeContent
            if (content.getTitle() != null) {
                ((TextView) adView.getHeadlineView()).setText(content.getTitle());
            }

            ...
            // Please follow the above method to fill the content of Icon, Large Picture, Call to Action, etc.
            ...

            // Call the YumiNativeAdView's setNativeAd method to register the NativeContent.

            adView.setNativeAd(content);

            // clean nativeAdContinerView
            nativeAdContinerView.removeAllViews();
            // add adView to nativeAdContinerView
            nativeAdContinerView.addView(adView);
        }
    }
}
```
3、Let's take a look at the individual tasks：

* before you show your native ads, please determine if native ads are expired：
```java
content.isExpired()
```
| return code | explain     | remarks                                                                             |
| ----------- | ----------- | ----------------------------------------------------------------------------------- |
| true        | expired     | this native ad has expired, showing ads that have expired will not generate revenue |
| false       | not expired | this native ads are valid                                                           |

* calls destroy() to destroy current content
```java
content.destroy() // note, this method is belong to NativeContent not to YumiNative
```

* Inflate the layout

```java
// Inflate XML layout，Its outermost node is YumiNativeAdView
YumiNativeAdView adView = (YumiNativeAdView) getLayoutInflater().inflate(R.layout.activity_native_material, null);
```

In this example, we're inflating an XML layout that contains views for displaying a unified native ad and then locating a reference to the YumiNativeAdView. 。

* Populate and register the asset views

This sample code locates the view used to display the headline, sets its text using the string asset provided by the ad object, and registers it with the YumiNativeAdView object：

```java
// get title view
TextView title = (TextView) adView.findViewById(R.id.headline)
// Locate the view that will hold the title, set its text, and call the YumiNativeAdView's setTitleViewmethod to register it.
adView.setTitleView(title);

// fill the title view using the string asset provided by NativeContent
if (content.getTitle() != null) {
    ((TextView) adView.getHeadlineView()).setText(content.getTitle());
}
```
This process of locating the view, setting its value, and registering it with the ad view class should be repeated for each of the assets provided by the native ad object that the app will display.

 * Register the native ad object：

This final step registers the native ad object with the view that's responsible for displaying it：

```java
adView.setNativeAd(content);
```

**Native video**
 
 1、If you want to show a video in a native ad, just add the layout of the video container (FrameLayout) in the view when you register the view and pass the container to the SDK.
 
 MediaContent（FrameLayout） can be defined in an XML layout or constructed dynamically. It should be placed within the view hierarchy of a YumiNativeAdView. Apps using a MediaContent don't need to populate it with an asset, but must register it with the YumiNativeAdView like this：

```java
 FrameLayout mediacontent = (FrameLayout) adView.findViewById(R.id.media_content);
 adView.setMediaLayout(mediacontent);
```
The MediaContent is a special View designed to display the main media asset. It has the following behavior：

* If the loaded ad has a video asset, the video is buffered and starts playing inside the mediacontent.

2、The following NativeContent interface can be used to determine whether the current NativeContent object has video material：

```java
content.getHasVideoContent()
```

**YumiNativeAdVideoController**

1、The YumiNativeAdVideoController class is used to retrieve information about video assets. Apps can get a reference to the controller from a NativeContent by calling the getNativeAdVideoController() method：

```java
YumiNativeAdVideoController nativeAdVideoController = content.getNativeAdVideoController();
```
This method always returns a YumiNativeAdVideoController object, even when no video asset is present in the ad。

YumiNativeAdVideoController offers these methods for querying video state：
 *  getAspectRatio() - Returns the aspect ratio of the video (width/height), or zero if no video asset is present。

2、Apps can also use the YumiNativeAdVideoController.YumiVideoLifecycleCallbacks class to get notifications when events occur in the lifecycle of a video asset：

```java
nativeAdVideoController.setVideoLifecycleCallbacks(
    new YumiNativeAdVideoController.YumiVideoLifecycleCallbacks() {
        @Override
        public void onVideoEnd() {
            super.onVideoEnd();
        }
    });
```

 **Implement in Activity lifecycle:**

```java
@Override
protected void onDestroy(){
    super.onDestroy();
    if (nativeAd != null) {
        nativeAd.onDestroy();
    }
}
```

## Other settings

You can use YumiNativeAdOptions object change the ads styles, as follows:

```java
YumiNativeAdOptions nativeAdOptions = new YumiNativeAdOptions.Builder()
                    .setIsDownloadImage(true)
                    .setAdChoicesPosition(YumiNativeAdOptions.POSITION_TOP_RIGHT)
                    .setAdAttributionPosition(YumiNativeAdOptions.POSITION_TOP_LEFT)
                    .setAdAttributionText("Ad")
                    .setAdAttributionTextColor(Color.argb(255, 255, 255, 255))
                    .setAdAttributionBackgroundColor(Color.argb(90, 0, 0, 0))
                    .setAdAttributionTextSize(10)
                    .setHideAdAttribution(false)
                    .setHideAdAttribution(new ExpressAdSize(400, 300)) // width: 400dp; height: 300dp
                    .build();
```
* **setIsDownloadImage** Image assets for native ads are returned via instances of NativeContent.Image, which holds a Drawable and a Url. If this option is set to true, the SDK fetches image assets automatically and populates both the Drawable and the Uri for you. If it's set to false, however, the SDK instead populates just the Url field, allowing you to download the actual images at your discretion.Default is true.
* **setAdChoicesPosition** use this property to specify where the AdChoicesView should be placed. Default is YumiNativeAdOptions.POSITION_TOP_RIGHT.
* **setAdAttributionPosition** use this property to specify where the Ad text view should be placed. Default is YumiNativeAdOptions.POSITION_TOP_LEFT.
* **setAdAttributionText** use this property to specify the Ad text. Default is “Ad”.
* **setAdAttributionTextColor** use this property to specify the Ad text color. Default is white.
* **setAdAttributionBackgroundColor** use this property to specify the Ad text background color。Default is gray.
* **setAdAttributionTextSize** use this property to specify the Ad text font size. Default is 10.
* **setHideAdAttribution** use this property to hide the Ad text. Default is display.
* **setHideAdAttribution(new ExpressAdSize(width, height))** pass the native ad container's size, the GDT network native ExpressAdView needs to set this property
