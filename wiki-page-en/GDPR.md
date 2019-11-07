# GDPR
This documentation is provided for compliance with the European Union's General Data Protection Regulation (GDPR). If you are collecting consent from your users, you can make use of APIs discussed below to inform YumiMediationSDK and some downstream consumers of this information. Get more information, please visit our official website.

## Set GDPR

GDPR state enumeration class definition

```java
enum YumiGDPRStatus {
    // The user has granted consent for personalized ads.
    PERSONALIZED,
    // The user has granted consent for non-personalized ads.
    NON_PERSONALIZED,
    // The user has neither granted nor declined consent for personalized or non-personalized ads.
    UNKNOWN
}
```

GDPR related methods
```java
// Set the GDPR status
YumiSettings.setGDPRConsent(YumiGDPRStatus.PERSONALIZED);

// Get GDPR status
 YumiSettings.getGDPRStatus();
```
## Networks informations
YumiMediationSDK will pass the GDPR status set in 5.3.1 to the three-party platform according to the official documentation of the three-party platform supporting GDPR, and the developer does not need to set additional. The following is the state of support for GDPR by each of the three parties.

|No.|platform|GDPR Support|remarks|
|---|---|---|---|
|1|adcolony|yes|[Official document](https://github.com/AdColony/AdColony-Android-SDK-3/wiki/GDPR#code-example)|
|2|admob|yes|[Official document](https://developers.google.com/admob/android/eu-consent#forward_consent_to_the_google_mobile_ads_sdk)|
|3|applovin|yes|[Official document](https://dash.applovin.com/docs/integration#androidPrivacySettings)|
|4|chartboost|yes|[Official document](https://answers.chartboost.com/en-us/child_article/android#gdpr)|
|5|inmobi|yes|[Official document](https://support.inmobi.com/monetize/android-guidelines/)|
|6|ineractive|yes||
|7|iqzone|yes||
|8|ironsource|yes|[Official document](https://developers.ironsrc.com/ironsource-mobile/android/advanced-settings/)|
|9|mintegral(-china)|yes|[Official document](http://cdn-adn.rayjump.com/cdn-adn/v2/markdown_v2/index.html?file=sdk-m_sdk-android&lang=en) |
|10|unity(-china)|yes|[Official document](https://unityads.unity3d.com/help/legal/gdpr)|
|11|vungle(-china)|yes|[Official document](https://support.vungle.com/hc/en-us/articles/360002922871-Get-Started-with-Vungle-Android-or-Amazon-SDK-v-6)|
|12|Yumi|yes||
|13|ZplayAds|yes||
|14|baidu|no||
|15|bytedance|no||
|16|facebook|*|Please check Facebook related [Official document](https://developers.facebook.com/docs/audience-network/android) |
|17|gdt|no||
|18|ksyun|no||
|19|oneway|no||
