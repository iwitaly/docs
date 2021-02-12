---
description: >-
  Learn how to get info about user subscription status and grant access to the
  premium features of the app using Adapty Android SDK
---

# Subscription Status

With Adapty you don't have to hardcode product ids to check subscription status. You just have to verify that the user has an active access level. To do this, you have to call **`.getPurchaserInfo()`** method:

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
Adapty.getPurchaserInfo { purchaserInfo, error ->
    if (error == null) {
        // check the accesss 
    }
}
```
{% endtab %}
{% endtabs %}

Request parameters:

* **Force update** \(optional\): a boolean indicating whether Adapty should fetch the data from API or get it from the local cache. Adapty SDK regularly refreshes the local data, so most of the time you don't have to use this flag. By default, it's set to `false`.

Response parameters:

* **Purchaser info**: a [**`PurchaserInfoModel`**](android-sdk-sdk-models.md#purchaserinfomodel) object. This model contains info about access levels, subscriptions, and non-subscription purchases. Generally, you have to check only access level status to determine whether the user has premium access to the app.

Below is a complete example of checking the user's access level.

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
Adapty.getPurchaserInfo { purchaserInfo, error ->
    if (error == null) {
        // "premium" is an identifier of default access level
        if (purchaserInfo?.accessLevels["premium"]?.isActive == true) {
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

You can respond to any changes in the user's subscription by setting an optional **`OnPurchaserInfoUpdatedListener`**. The callback will fire whenever we receive a change in purchaser info:

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
Adapty.setOnPurchaserInfoUpdatedListener(object : OnPurchaserInfoUpdatedListener {
    override fun onPurchaserInfoReceived(purchaserInfo: PurchaserInfoModel) {
        // handle any changes to subscription state
    }
})
```
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
Make sure to set up [Real-time developer notifications \(RTDN\)](../../../settings/android-sdk.md#real-time-developer-notifications-rtdn) to receive subscription updates without significant delays.
{% endhint %}

