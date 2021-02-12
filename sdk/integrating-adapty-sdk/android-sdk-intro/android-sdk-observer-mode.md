---
description: >-
  Learn how to use Adapty Android SDK in Observer mode along with existing
  purchase infrastructure
---

# Observer Mode

If you have a functioning subscription system and want to give Adapty SDK a quick try, you can use Observer mode. With just a couple of lines of code you can:

* get insights by using our top-class [analytics](../../../analytics/advanced-analytics.md);
* send subscription [events](../../../analytics/integrations/events.md) to your [server](../../../analytics/integrations/webhook.md) and [3rd party services](../../../analytics/integrations/3rd-party-analytics.md);
* view and analyze customers in Adapty [CRM](../../../profiles-and-promo-campaigns/profiles.md).

At any purchase or restore in your application, you need to call .**`restorePurchases()`** method to record the action in Adapty.

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
Adapty.restorePurchases { purchaserInfo, googleValidationResultList, error ->
    if (error == null) {
        // successful restore
    }
}
```
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
When running in Observer mode, Adapty SDK won't consume or acknowledge any purchases, so make sure you're handling it. Otherwise, the purchases will be automatically refunded after 3 days.
{% endhint %}



### A/B tests analytics

In Observer mode, Adapty SDK doesn't know, where the purchase was made from. If you display products using our [Paywalls](../../../purchase-infrastructure/paywall.md) or [A/B tests](../../../purchase-infrastructure/ab-tests.md), you can manually assign variation to the purchase. After doing this, you'll be able to see metrics in Adapty Dashboard.

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
Adapty.setTransactionVariationId(transactionId, variationId) { error ->
    if (error == null) {
        // success
    }
}
```
{% endtab %}
{% endtabs %}

Request parameters:

* **Transaction Id** \(required\): a string identifier \(**`purchase.getOrderId()`**\) of the purchase, where the purchase is an instance of the billing library [Purchase](https://developer.android.com/reference/com/android/billingclient/api/Purchase) class.
* **Variation Id** \(required\): a string identifier of the variation. You can get it using **`variationId`** property of [**`PaywallModel`**](android-sdk-sdk-models.md#paywallmodel).

