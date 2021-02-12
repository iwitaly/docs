---
description: >-
  Learn how to pass attribution data to the dashboard using Adapty Android SDK.
  Adapty supports AppsFlyer, Adjust, and Branch
---

# Attribution Integration

Adapty allows easy integration with the popular attribution services: [AppsFlyer](android-sdk-attribution-integration.md#appsflyer), [Adjust](android-sdk-attribution-integration.md#adjust), and [Branch](android-sdk-attribution-integration.md#branch). Adapty will send subscription events to these services so you can accurately measure the performance of ad campaigns. You can also filter analytics using attribution data.

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
{% tab title="Kotlin" %}
```swift
Adapty.updateAttribution(attribution, source, networkUserId) { error ->
    if (error == null) {
        // succesfull attribution update
    }
}
```
{% endtab %}
{% endtabs %}

Request parameters:

* **Attribution** \(required\): a dictionary containing attribution \(conversion\) data.
* **Source** \(required\): a source of attribution. The allowed values are:
  * **`AttributionType.APPSFLYER`**
  * **`AttributionType.ADJUST`**
  * **`AttributionType.BRANCH`**
  * **`AttributionType.CUSTOM`**
* **Network user Id** \(optional\): a string profile's identifier from the attribution service.



### AppsFlyer

To set attribution from AppsFlyer, pass the attribution you receive from **`AppsFlyerConversionListener`** of AppsFlyer Android SDK. Don't forget to set **`networkUserId`**. You should also configure [AppsFlyer integration](../../../analytics/integrations/3rd-party-analytics.md#appsflyer) in Adapty Dashboard.

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
val conversionListener: AppsFlyerConversionListener = object : AppsFlyerConversionListener {
    override fun onConversionDataSuccess(conversionData: Map<String, Any>) {
        // It's important to include the network user ID
        Adapty.updateAttribution(
            conversionData,
            AttributionType.APPSFLYER,
            AppsFlyerLib.getInstance().getAppsFlyerUID(context)
        )
    }
}
```
{% endtab %}
{% endtabs %}



### Adjust

To set attribution from Adjust, pass the attribution you receive from **`OnAttributionChangedListener`** of Adjust Android SDK. You should also configure [Adjust integration](../../../analytics/integrations/3rd-party-analytics.md#adjust) in Adapty Dashboard.

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
val config = AdjustConfig(context, adjustAppToken, environment)
config.setOnAttributionChangedListener { attribution ->
    attribution?.let { attribution ->
        Adapty.updateAttribution(attribution, AttributionType.ADJUST)
    }
}
Adjust.onCreate(config)
```
{% endtab %}
{% endtabs %}



### Branch

To connect Branch user and Adapty user, make sure you set your **`customerUserId`** as Branch Identity Id. If you prefer to not use **`customerUserId`** in Branch, set **`networkUserId`** param in **`.updateAttribution()`** method to specify the Branch user Id. You should also configure [Branch integration](../../../analytics/integrations/3rd-party-analytics.md#branch) in Adapty Dashboard.

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
// login and update attribution
Branch.getAutoInstance(this)
    .setIdentity("YOUR_USER_ID") { referringParams, error ->
        referringParams?.let { params ->
            Adapty.updateAttribution(params, AttributionType.BRANCH)
        }
    }

// logout
Branch.getAutoInstance(context).logout()
```
{% endtab %}
{% endtabs %}

