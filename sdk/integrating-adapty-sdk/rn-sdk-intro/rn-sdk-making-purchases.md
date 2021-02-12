---
description: >-
  Learn how to make and restore mobile purchases using Adapty React Native SDK.
  Adapty handles server-side validation, including renewals and grace periods
---

# Making Purchases

To make the purchase, call **`adapty.purchases.makePurchase()`** method:

{% tabs %}
{% tab title="TypeScript" %}
```typescript
try {
  const {
		receipt,
		purchaserInfo,
		product,
	} = await adapty.purchases.makePurchase(product);
} 
catch (error: AdaptyError) {}
```
{% endtab %}
{% endtabs %}

Request parameters:

* **`product`** — **`AdaptyProduct`** retrieved from a paywall

Response parameters:

* **`purchaserInfo` — Purchaser info**: an **`AdaptyPurchaserInfo`** object. It contains info about access levels, subscriptions, and non-subscription purchases. Generally, you have to check only access level status to determine whether the user has premium access to the app
* **`receipt` — Receipt**: a string representation of a receipt
* **`product` — Product**: an **`AdaptyProduct`**  object you've passed to this method

{% hint style="warning" %}
Make sure you've added [App Store Connect shared secret](../../../settings/ios-sdk.md#app-store-connect-shared-secret) for iOS and uploaded [Service Account key file](../../../settings/android-sdk.md#service-account-key-file) for Android in Adapty Dashboard, without them, we can't validate purchases.
{% endhint %}

Below is a complete example of making the purchase and checking the user's access level.

{% tabs %}
{% tab title="TypeScript" %}
```typescript
try {
  const { purchaserInfo } = await adapty.purchases.makePurchase(product);
  // "premium" is an identifier of default access level
  if (purchaserInfo?.accessLevels['premium'].isActive) {
    // grant access to premium features
  }
} catch (error: AdaptyError) {}
```
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
Make sure to set up [URL for App Store Server Notifications](../../../settings/ios-sdk.md#app-store-connect-subscription-status-url) for iOS and  [Real-time developer notifications \(RTDN\)](../../../settings/android-sdk.md#real-time-developer-notifications-rtdn) for Android to receive subscription updates without significant delays.
{% endhint %}



### Restoring purchases

To restore purchases call **`adapty.purchases.restore()`** method:

{% tabs %}
{% tab title="TypeScript" %}
```typescript
try {
  const {
    purchaserInfo
    receipt,
    googleValidationResults,
  } = await adapty.purchases.restore()
} catch (error: AdaptyError) {}
```
{% endtab %}
{% endtabs %}

Response parameters:

* **`purchaserInfo`** — **Purchaser info**: an **`AdaptyPurchaserInfo`** object. It contains info about access levels, subscriptions, and non-subscription purchases. Generally, you have to check only access level status to determine whether the user has premium access to the app.
* **`receipt`** — String representation of Apple receipts. Might be null.
* **`googleValidationResults`** — Array of stringed representation of PlayMarket receipts. Might be null.

