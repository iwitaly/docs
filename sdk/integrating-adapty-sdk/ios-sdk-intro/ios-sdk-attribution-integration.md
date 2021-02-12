---
description: >-
  Learn how to pass attribution data to the dashboard using Adapty iOS SDK.
  Adapty supports AppsFlyer, Adjust, Branch, and Apple Search Ads
---

# Attribution Integration

Adapty allows easy integration with the popular attribution services: [AppsFlyer](ios-sdk-attribution-integration.md#appsflyer), [Adjust](ios-sdk-attribution-integration.md#adjust), [Branch](ios-sdk-attribution-integration.md#branch), and [Apple Search Ads](ios-sdk-attribution-integration.md#apple-search-ads). Adapty will send [subscription events](../../../analytics/integrations/) to these services so you can accurately measure the performance of ad campaigns. You can also filter [analytics](../../../analytics/advanced-analytics.md) using attribution data.

{% hint style="warning" %}
Make sure to turn off sending subscription events from devices and your server to avoid duplication. If you set up direct integration with Facebook, turn off events forwarding from AppsFlyer, Adjust, or Branch.
{% endhint %}

{% hint style="warning" %}
Make sure you've set up [attribution integration](../../../analytics/integrations/3rd-party-analytics.md) in Adapty Dashboard, otherwise we won't be able to send subscription events.
{% endhint %}

{% hint style="info" %}
Attribution data is set for every profile one time, we won't override the data once it's been saved.
{% endhint %}

To set attribution data for the profile, use **`.updateAttribution()`** method:

{% tabs %}
{% tab title="Swift" %}
```swift
Adapty.updateAttribution("<attribution>", source: "<source>", networkUserId: "<networkUserId>") { (error) in
    if error == nil {
        // succesfull attribution update
    }
}
```
{% endtab %}
{% endtabs %}

Request parameters:

* **Attribution** \(required\): a dictionary containing attribution \(conversion\) data.
* **Source** \(required\): a source of attribution. The allowed values are:
  * **`.appsflyer`**
  * **`.adjust`**
  * **`.branch`**
  * **`.custom`**
* **Network user Id** \(optional\): a string profile's identifier from the attribution service.



### AppsFlyer

To set attribution from AppsFlyer, pass the attribution you receive from the delegate method of AppsFlyer iOS SDK. Don't forget to set **`networkUserId`**. You should also configure [AppsFlyer integration](../../../analytics/integrations/3rd-party-analytics.md#appsflyer) in Adapty Dashboard.

{% tabs %}
{% tab title="Swift" %}
```swift
import AppsFlyerLib

// AppsFlyer v5 (AppsFlyerTrackerDelegate)
extension AppDelegate: AppsFlyerTrackerDelegate {
    func onConversionDataSuccess(_ conversionInfo: [AnyHashable : Any]) {
        // It's important to include the network user ID
        Adapty.updateAttribution(conversionInfo, source: .appsflyer, networkUserId: AppsFlyerTracker.shared().getAppsFlyerUID())
    }
}

// AppsFlyer v6 (AppsFlyerLibDelegate)
extension AppDelegate: AppsFlyerLibDelegate {
    func onConversionDataSuccess(_ installData: [AnyHashable : Any]) {
        // It's important to include the network user ID
        Adapty.updateAttribution(installData, source: .appsflyer, networkUserId: AppsFlyerLib.shared().getAppsFlyerUID())
    }
}
```
{% endtab %}
{% endtabs %}



### Adjust

To set attribution from Adjust, pass the attribution you receive from the delegate method of Adjust iOS SDK. You should also configure [Adjust integration](../../../analytics/integrations/3rd-party-analytics.md#adjust) in Adapty Dashboard.

{% tabs %}
{% tab title="Swift" %}
```swift
import Adjust

extension AppDelegate: AdjustDelegate {
    func adjustAttributionChanged(_ attribution: ADJAttribution?) {
        if let attribution = attribution?.dictionary() {
            Adapty.updateAttribution(attribution, source: .adjust)
        }
    }
}
```
{% endtab %}
{% endtabs %}



### Branch

To connect Branch user and Adapty user, make sure you set your **`customerUserId`** as Branch Identity Id. If you prefer to not use **`customerUserId`** in Branch, set **`networkUserId`** param in **`.updateAttribution()`** method to specify the Branch user Id.

{% tabs %}
{% tab title="Swift" %}
```swift
// login
Branch.getInstance().setIdentity("YOUR_USER_ID")

// logout
Branch.getInstance().logout()
```
{% endtab %}
{% endtabs %}

Next, pass the attribution you receive from the initializing method of Branch iOS SDK to Adapty.

{% tabs %}
{% tab title="Swift" %}
```swift
import Branch

Branch.getInstance().initSession(launchOptions: launchOptions) { (data, error) in
    if let data = data {
        Adapty.updateAttribution(data, source: .branch)
    }
}
```
{% endtab %}
{% endtabs %}

You should also configure [Branch integration](../../../analytics/integrations/3rd-party-analytics.md#branch) in Adapty Dashboard.



### Apple Search Ads

Adapty can automatically collect Apple Search Ad attribution data. All you need is to add **`AdaptyAppleSearchAdsAttributionCollectionEnabled`** to the app’s **`Info.plist`** file and set it to **`YES`** \(boolean value\).

