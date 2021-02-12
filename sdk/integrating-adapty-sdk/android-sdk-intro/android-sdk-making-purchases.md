---
description: >-
  Learn how to make and restore mobile purchases using Adapty Android SDK.
  Adapty handles server-side validation, including renewals and grace periods
---

# Making Purchases

To make the purchase, you have to call **`.makePurchase()`** method:

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
Adapty.makePurchase(activity, product) { purchaserInfo, purchaseToken, googleValidationResult, product, error ->
    if (error == null) {
        // successful purchase
    }
}
```
{% endtab %}
{% endtabs %}

Request parameters:

* **Product** \(required\): a [**`ProductModel`**](android-sdk-sdk-models.md#productmodel) object retrieved from the paywall.

Response parameters:

* **Purchaser info**: a [**`PurchaserInfoModel`**](android-sdk-sdk-models.md#purchaserinfomodel) object. This model contains info about access levels, subscriptions, and non-subscription purchases. Generally, you have to check only access level status to determine whether the user has premium access to the app.
* **Purchase token**: a string purchase token of the transaction from Google Play used to validate the purchase.
* **Google validation result**: a dictionary containing raw validation result of [subscription](https://developers.google.com/android-publisher/api-ref/rest/v3/purchases.subscriptions) or [product](https://developers.google.com/android-publisher/api-ref/rest/v3/purchases.products) from Google.
* **Product**: a [**`ProductModel`**](android-sdk-sdk-models.md#productmodel) object you've passed to this method.

{% hint style="warning" %}
Make sure you've uploaded [Service Account key file](../../../settings/android-sdk.md#service-account-key-file) ****in Adapty Dashboard, without it, we can't validate purchases.
{% endhint %}

Below is a complete example of making the purchase and checking the user's access level.

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
Adapty.makePurchase(activity, product) { purchaserInfo, purchaseToken, googleValidationResult, product, error ->
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

{% hint style="warning" %}
Make sure to set up [Real-time developer notifications \(RTDN\)](../../../settings/android-sdk.md#real-time-developer-notifications-rtdn) to receive subscription updates without significant delays.
{% endhint %}

### 

### Restoring purchases

To restore purchases, you have to call **`.restorePurchases()`** method:

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

Response parameters:

* **Purchaser info**: a [**`PurchaserInfoModel`**](android-sdk-sdk-models.md#purchaserinfomodel) object. This model contains info about access levels, subscriptions, and non-subscription purchases. Generally, you have to check only access level status to determine whether the user has premium access to the app.
* **Google validation result**: a list containing raw validation results of [subscription](https://developers.google.com/android-publisher/api-ref/rest/v3/purchases.subscriptions) or [product](https://developers.google.com/android-publisher/api-ref/rest/v3/purchases.products) from Google Play.

In [Observer mode](android-sdk-observer-mode.md), after any purchase or restore in your application, you should call **`.restorePurchases()`** method to record the action in Adapty.

