---
description: >-
  Learn how to make and restore mobile purchases using Adapty Flutter SDK.
  Adapty handles server-side validation, including renewals and grace periods
---

# Making Purchases

To make the purchase, you have to call **`.makePurchase()`** method:

{% tabs %}
{% tab title="Flutter" %}
```dart
try {
	final MakePurchaseResult makePurchaseResult = await Adapty.makePurchase(product);
} on AdaptyError catch (adaptyError) {}
catch (e) {}
```
{% endtab %}
{% endtabs %}

Request parameters:

* **Product** \(required\): an **`AdaptyProduct`** object retrieved from the paywall.

Response parameters:

* **Purchaser info**: an **`AdaptyPurchaserInfo`** object. This model contains info about access levels, subscriptions, and non-subscription purchases. Generally, you have to check only access level status to determine whether the user has premium access to the app.

{% hint style="warning" %}
Make sure you've added [App Store Connect shared secret](../../../settings/ios-sdk.md#app-store-connect-shared-secret) for iOS and uploaded [Service Account key file](../../../settings/android-sdk.md#service-account-key-file) for Android in Adapty Dashboard, without them, we can't validate purchases.
{% endhint %}

Below is a complete example of making the purchase and checking the user's access level.

{% tabs %}
{% tab title="Flutter" %}
```dart
try {
  final MakePurchaseResult makePurchaseResult = await Adapty.makePurchase(product);
  // "premium" is an identifier of default access level
  if (makePurchaseResult?.purchaserInfo?.accessLevels['premium'].isActive) {
  	// grant access to premium features
  }
} on AdaptyError catch (adaptyError) {}
catch (e) {}
```
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
Make sure to set up [URL for App Store Server Notifications](../../../settings/ios-sdk.md#app-store-connect-subscription-status-url) for iOS and  [Real-time developer notifications \(RTDN\)](../../../settings/android-sdk.md#real-time-developer-notifications-rtdn) for Android to receive subscription updates without significant delays.
{% endhint %}



### Restoring purchases

To restore purchases, you have to call **`.restorePurchases()`** method:

{% tabs %}
{% tab title="Flutter" %}
```dart
try {
	final RestorePurchasesResult restorePurchasesResult = await Adapty.restorePurchases();
} on AdaptyError catch (adaptyError) {}
catch (e) {}
```
{% endtab %}
{% endtabs %}

Response parameters:

* **Purchaser info**: an **`AdaptyPurchaserInfo`** object. This model contains info about access levels, subscriptions, and non-subscription purchases. Generally, you have to check only access level status to determine whether the user has premium access to the app.



### Deferred purchases \(iOS only\)

{% tabs %}
{% tab title="Flutter" %}
```dart
try {
	final MakePurchaseResult makePurchaseResult = await makeDeferredPurchase("<productId>");
} on AdaptyError catch (adaptyError) {}
catch (e) {}
```
{% endtab %}
{% endtabs %}

