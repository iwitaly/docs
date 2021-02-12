---
description: >-
  Learn how to get info about user subscription status and grant access to the
  premium features of the app using Adapty iOS SDK
---

# Subscription Status

With Adapty you don't have to hardcode product ids to check subscription status. You just have to verify that the user has an active access level. To do this, you have to call **`.getPurchaserInfo()`** method:

{% tabs %}
{% tab title="Swift" %}
```swift
Adapty.getPurchaserInfo(forceUpdate: Bool) { (purchaserInfo, error) in
    if error == nil {
        // check the accesss 
    }
}
```
{% endtab %}
{% endtabs %}

Request parameters:

* **Force update** \(optional\): a boolean indicating whether Adapty should fetch the data from API or get it from the local cache. Adapty SDK regularly refreshes the local data, so most of the time you don't have to use this flag. By default, it's set to `false`.

Response parameters:

* **Purchaser info**: a [**`PurchaserInfoModel`**](ios-sdk-models.md#purchaserinfomodel) object. This model contains info about access levels, subscriptions, and non-subscription purchases. Generally, you have to check only access level status to determine whether the user has premium access to the app.

Below is a complete example of checking the user's access level.

{% tabs %}
{% tab title="Swift" %}
```swift
Adapty.getPurchaserInfo { (purchaserInfo, error) in
    if error == nil {
        // "premium" is an identifier of default access level
        if purchaserInfo?.accessLevels["premium"]?.isActive == true {
            // grant access to premium features
        }
    }
}
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
You can have multiple access levels per app. For example, if you have a newspaper app and sell subscriptions to different topics independently, you can create access levels "sports" and "science". But most of the time, you will only need one access level, in that case, you can just use the default "**premium**" access level.

Read more about access levels in the [Access Level](../../../purchase-infrastructure/access-level.md) section.
{% endhint %}



### Listening for subscription status updates

Whenever the user's subscription changes, Adapty will fire an event. To receive subscription updates, extend **`AdaptyDelegate`** with **`didReceiveUpdatedPurchaserInfo`** method:

{% tabs %}
{% tab title="Swift" %}
```swift
extension AppDelegate: AdaptyDelegate {
    
    func didReceiveUpdatedPurchaserInfo(_ purchaserInfo: PurchaserInfoModel) {
        // handle any changes to subscription state
    }
    
}
```
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
Make sure to set up [URL for App Store Server Notifications](../../../settings/ios-sdk.md#app-store-connect-subscription-status-url) to receive subscription updates without significant delays.
{% endhint %}

