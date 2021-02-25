---
description: >-
  Learn how to set up integration with external analytics using Adapty iOS SDK.
  Adapty supports  Amplitude, Mixpanel, Facebook Ads, and AppMetrica
---

# Analytics Integration

Adapty sends all [subscription events](../../../analytics/integrations/#events) to analytical services, such as [Amplitude](../../../analytics/integrations/3rd-party-analytics.md#amplitude), [Mixpanel](../../../analytics/integrations/3rd-party-analytics.md#mixpanel), [Facebook Ads](../../../analytics/integrations/3rd-party-analytics.md#facebook-ads), [AppMetrica](../../../analytics/integrations/3rd-party-analytics.md#appmetrica). We can also send events to your server using [webhook integration](../../../analytics/integrations/webhook.md). The best thing about this is that you don't have to send any of the events, we'll do it for you. Just make sure to [configure](../../../analytics/integrations/3rd-party-analytics.md) the integration in Adapty Dashboard.

The only thing you have to do is to set the profile's identifier for the selected analytics using [**`.updateProfile()`**](ios-sdk-setting-user-attributes.md) method. For example, for Amplitude integration, you can set either **`amplitudeUserId`** or **`amplitudeUserId`**. For Mixpanel integration, you have to set **`mixpanelUserId`**. When these identifiers are not set, Adapty will use [**`customerUserId`**](ios-sdk-identifying-users.md) instead. If the **`customerUserId`** is not set, we will use our internal profile id.

{% hint style="warning" %}
Make sure to turn off sending subscription events from devices and your server to avoid duplication. If you set up direct integration with Facebook, turn off forwarding events from AppsFlyer, Adjust, or Branch.
{% endhint %}

{% hint style="warning" %}
Since iOS 14 and IDFA changes, if you use Facebook integration, make sure you send [**`facebookAnonymousId`**](https://developers.facebook.com/docs/reference/iossdk/current/FBSDKCoreKit/classes/fbsdkappevents.html/) to Adapty via [**`.updateProfile()`**](ios-sdk-setting-user-attributes.md) method. It allows Facebook to handle ads traffic if IDFA is not available.

```swift
import AdSupport

let params = ProfileParameterBuilder().withFacebookAnonymousId(FBSDKCoreKit.AppEvents.anonymousID)
Adapty.updateProfile(params: params) { (error) in    
    if error == nil {        
        // successful update                                  
    }
}
```
{% endhint %}

By default, all subscription events will be forwarded to external analytics of your choice. You can configure them in the [Integrations](../../../analytics/integrations/) section. If you want to stop sending analytics events for a specific customer, you can disable external analytics for him using **`.setExternalAnalyticsEnabled()`** method:

{% tabs %}
{% tab title="Swift" %}
```swift
Adapty.setExternalAnalyticsEnabled(enabled)
```
{% endtab %}
{% endtabs %}

Request parameters:

* **Enabled** \(required\): a boolean indicating whether external analytics should be enabled or not.

