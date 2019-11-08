## Mediation Test Suite

YUMI SDK provideds a test mode to test your 3rd-party Integrations.

<img src="https://github.com/yumimobi/YumiMediationSDKDemo-Android-wiki/blob/master/docs/document/image10.png" alt="img3">

1、Call method to open test page :
```java
YumiSettings.startDebugging(Activity, BannerSlotID, InterstitialSlotID, MediaSlotID, NativeSloatID, SplashSlotID); 
```

If you set the version, channel, according to your need to set the channel in the platform configuration, version call method to open the debug page:

YumiSettings.startDebugging (Activity, BannerSlotID, InterstitialSlotID, MediaSlotID, NativeSloatID, SplashSlotID, channelID, versionName);

2、The Yumi SDK will detect the platform accessed in the application and display the acquired platform in the platform list, and go to the debug page:

  1）debug page：

<img src="https://github.com/yumimobi/YumiMediationSDKDemo-Android-wiki/blob/master/docs/document/image08.png" alt="img4" width="200" height="355">
 
 debug page explain:

 * If the platform name is not displayed in the platform list，explain that the developer no add  this 
platform

 * If the platform name is green, the Yumi server have configured this platform
 * If the platform name is gray, the Yumi server not have configured this platform

3、If the platform name is gray，click this platform, will show warning：

<img src="https://github.com/yumimobi/YumiMediationSDKDemo-Android-wiki/blob/master/docs/document/image09.png" alt="img4" width="200" height="355">

4、If the platform name is green, you can click on this platform to debug:

  1）When SDK Available is green, it means that the three-party platform adapter has been added. When it is red, it indicates that the three-party platform adapter has not been added. Go back to Add lib file to check whether the platform adapter has been added

  2）When the Configuration present is green, the three-party platform adapter Manifest is registered. When it is red, it means that the Manifest of the three-party platform adapter component is not registered, which can be returned to Add permission to check whether the platform adapter component has been added

  3）Failed SDK to start or No_fill is green to indicate that the advertisement has been shown successfully. When it is red, it means that the advertisement has not been shown successfully. You can proceed to the next step. If all the steps are not red after completion, please email us at support@yumimobi.com

<img src="https://github.com/yumimobi/YumiMediationSDKDemo-Android-wiki/blob/master/docs/document/image06.jpg" alt="img4" width="200" height="355">

5、Demand Available? Click Fetch to request ad. A fetch will generate an ad download.  You will get a text response confirming the ad download, or instead an error.

6、Ad Displayed? Click Show to display an ad.  When ad shows properly, all test elements will turn green, which indicates this platform has been integrated successfully, at least for that ad type.

Below is a sample screen of some banner ads that were fetched from Baidu ad network and displayed.  The HIDE button simple allows the developer to test the SDK’s hide feature.

<img src="https://github.com/yumimobi/YumiMediationSDKDemo-Android-wiki/blob/master/docs/document/image07.jpg" alt="img4" width="200" height="355">

7、The debugging mode must be completed before releasing the App.

## Test ID
| Formats | Slot(Placement) ID | Note |
| --- | --- | --- |
| Banner | uz852t89 | Using this test ID, you are able to get test ads which are from YUMI, AdMob, AppLovin, Baidu, IQzone  |
| Interstitial | 56ubk22h | Using this test ID, you are able to get test ads which are form YUMI, AdMob, AppLovin, Baidu, IronSource, InMobi, IQzone, Unity Ads, Vungle, ZPLAYAds |
| Rewarded Video | ew9hyvl4 | Using this test ID, you can get test ads which are from YUMI, AdMob, AppLovin, GDTMob, IronSource, InMobi, IQzone, Unity Ads, Vungle, ZPLAYAds |
| Native | dt62rndy | You can get test ads which are from YUMI, AdMob, Baidu, GDTMob, Facebook by using this test ID |
| Splash | vv7snvc5 | You can get test ads which are from YUMI, Baidu, GDTMob, BytedanceAds by using this test ID |

[Frequently asked questions](https://github.com/yumimobi/Developer-doc/blob/master/FAQ_latest_en.md) in the integration.

## Q&A
If you meet any issue when integrating, click to see [YumiMediationSDK Q&A](https://github.com/yumimobi/Developer-doc/blob/master/FAQ_latest_en.md).