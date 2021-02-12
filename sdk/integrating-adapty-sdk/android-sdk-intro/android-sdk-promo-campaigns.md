---
description: >-
  Learn how to display personalized promo offers to your customers using Adapty
  Android SDK
---

# Promo Campaigns

[Promo Campaigns](../../../profiles-and-promo-campaigns/promo-campaigns.md) help you to increase revenue with targeted offers for your customers. You can use them to upsell, convert freemium users to paid ones, and win back churned subscribers.

{% hint style="warning" %}
Make sure to set [Firebase Cloud Messaging \(FCM\) server key](../../../settings/android-sdk.md#push-notifications) in Adapty Dashboard, without it, we can't send push notifications.
{% endhint %}

To get an available promo offer for the user, call **`.getPromo()`** method:

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
Adapty.getPromo { promo, error ->
    if (error == null && promo != null) {
        // handle available promo
    }
}
```
{% endtab %}
{% endtabs %}

Response parameters:

* **Promo**: a [**`PromoModel`**](android-sdk-sdk-models.md#promomodel) object. This model contains info about the available promo offer. It can be null when there's no offer available \(which is fine\). 



### Listening for promo updates

You can respond to any changes in the user's promo by setting an optional **`OnPromoReceivedListener`**. The callback will fire whenever we receive a change in the promo:

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
Adapty.setOnPromoReceivedListener(object : OnPromoReceivedListener {

    override fun onPromoReceived(promo: Promo) {
        // handle available promo
    }

})
```
{% endtab %}
{% endtabs %}



### Configuring push notifications

Check the [Push Notifications](push-notifications.md) section to get instructions on configuring push notifications.

