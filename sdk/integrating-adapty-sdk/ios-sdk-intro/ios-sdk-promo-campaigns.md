---
description: >-
  Learn how to display personalized promo offers to your customers using Adapty
  iOS SDK
---

# Promo Campaigns

[Promo Campaigns](../../../profiles-and-promo-campaigns/promo-campaigns.md) help you to increase revenue with targeted offers for your customers. You can use them to upsell, convert freemium users to paid ones, and win back churned subscribers.

{% hint style="warning" %}
Make sure to upload the [push certificate](../../../settings/ios-sdk.md#push-notifications) in Adapty Dashboard, without it, we can't send push notifications.
{% endhint %}

To get an available promo offer for the user, call **`.getPromo()`** method:

{% tabs %}
{% tab title="Swift" %}
```swift
Adapty.getPromo { (promo, error) in
    if (error == nil && promo != nil) {
        // handle available promo
    }
}
```
{% endtab %}
{% endtabs %}

Response parameters:

* **Promo**: a [**`PromoModel`**](ios-sdk-models.md#promomodel) object. This model contains info about the available promo offer. It can be null when there's no offer available \(which is fine\). 



### Listening for promo updates

Whenever the user's promo offer changes, Adapty will fire an event. To receive promo offers updates, extend **`AdaptyDelegate`** using **`didReceivePromo`** method:

{% tabs %}
{% tab title="Swift" %}
```swift
extension AppDelegate: AdaptyDelegate {
    
    func didReceivePromo(_ promo: PromoModel) {
        // handle available promo
    }
    
}
```
{% endtab %}
{% endtabs %}



### Handling push notifications

You have to pass push notifications to Adapty SDK, so it can handle promo notifications and respond accordingly. Here's an example of doing this:

{% tabs %}
{% tab title="Swift" %}
```swift
func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any], fetchCompletionHandler completionHandler: @escaping (UIBackgroundFetchResult) -> Void) {
    Adapty.handlePushNotification(userInfo) { (_) in
        completionHandler(UIBackgroundFetchResult.newData)
    }
}
```
{% endtab %}
{% endtabs %}

