本文件是为遵守欧洲联盟的一般数据保护条例（GDPR）而提供的。 自 YumiMediationSDK 4.1.0 起，如果您正在收集用户的信息，您可以使用下面提供的 API 将此信息通知给 YumiMediationSDK 和部分三方平台。更多信息请查看我们的官网。

## 设置 GDPR

GDPR 状态枚举类定义

```java
enum YumiGDPRStatus {
    // 用户已授予个性化广告的同意权
    PERSONALIZED,
    // 用户已授予非个性化广告的同意权
    NON_PERSONALIZED,
    // 默认设置，用户未设置 GDPR 状态
    UNKNOWN
}
```

GDPR 相关方法
```java
// 设置 GDPR 状态
YumiSettings.setGDPRConsent(YumiGDPRStatus.PERSONALIZED);

// 获取 GDPR 状态
 YumiSettings.getGDPRStatus();
```
## 支持 GDPR 的平台
YumiMediationSDK 会将 5.3.1 中设置的 GDPR 状态根据支持 GDPR 的三方平台的官方文档设置到各三方平台，开发者无需额外设置。以下是各三方平台对 GDPR 的支持状态。

|序号|平台|是否支持 GDPR|备注|
|---|---|---|---|
|1|adcolony|是|[官方文档](https://github.com/AdColony/AdColony-Android-SDK-3/wiki/GDPR#code-example)|
|2|admob|是|[官方文档](https://developers.google.com/admob/android/eu-consent#forward_consent_to_the_google_mobile_ads_sdk)|
|3|applovin|是|[官方文档](https://dash.applovin.com/docs/integration#androidPrivacySettings)|
|4|chartboost|是|[官方文档](https://answers.chartboost.com/en-us/child_article/android#gdpr)|
|5|inmobi|是|[官方文档](https://support.inmobi.com/monetize/android-guidelines/)|
|6|ineractive|是||
|7|iqzone|是||
|8|ironsource|是|[官方文档](https://developers.ironsrc.com/ironsource-mobile/android/advanced-settings/)|
|9|mintegral(-china)|是|[官方文档](http://cdn-adn.rayjump.com/cdn-adn/v2/markdown_v2/index.html?file=sdk-m_sdk-android&lang=en) |
|10|unity(-china)|是|[官方文档](https://unityads.unity3d.com/help/legal/gdpr)|
|11|vungle(-china)|是|[官方文档](https://support.vungle.com/hc/en-us/articles/360002922871-Get-Started-with-Vungle-Android-or-Amazon-SDK-v-6)|
|12|Yumi|是||
|13|ZplayAds|是||
|14|baidu|否||
|15|bytedance|否||
|16|facebook|*|请查阅 Facebook 相关[官方文档](https://developers.facebook.com/docs/audience-network/android) |
|17|gdt|否||
|18|ksyun|否||
|19|oneway|否||