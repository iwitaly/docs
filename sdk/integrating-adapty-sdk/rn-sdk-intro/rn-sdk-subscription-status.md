---
description: >-
  Learn how to get info about user subscription status and grant access to the
  premium features of the app using Adapty React Native SDK
---

# Subscription Status

With Adapty you don't have to hardcode product ids to check subscription status. You just have to verify that the user has an active access level. To do this, you have to call **`adapty.purchases.getInfo()`** method:

{% tabs %}
{% tab title="TypeScript" %}
```typescript
try {
  const info = await adapty.purchases.getInfo({ forceUpdate: false })
} catch (error: AdaptyError) {}
```
{% endtab %}
{% endtabs %}

Request parameters:

* **`{forceUpdate}`**  — **Force update**. Optional. If you want to force fetching from the server. Data from a local cache would be used otherwise.

Response parameters:

* **`info`** — **Purchaser info**: an **`AdaptyPurchaserInfo`** object. It contains info about access levels, subscriptions, and non-subscription purchases. Generally, you have to check only access level status to determine whether the user has premium access to the app.

Below is a complete example of checking the user's access level.

{% tabs %}
{% tab title="TypeScript" %}
```typescript
try {
  const info = await adapty.purchases.getInfo();
  // "premium" is an identifier of default access level
  if (info?.accessLevels['premium']?.isActive) {
	  // grant access to premium features
  }
} catch (error: AdaptyError) {}
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
You can have multiple access levels per app. For example, if you have a newspaper app and sell subscriptions to different topics independently, you can create access levels "sports" and "science". But most of the time, you will only need one access level, in that case, you can just use the default "**premium**" access level.

Read more about access levels in the [Access Level](../../../purchase-infrastructure/access-level.md) section.
{% endhint %}



### Listening for subscription status updates

{% tabs %}
{% tab title="TypeScript" %}
```typescript
useEffect(() => {
  adapty.addEventListener('onInfoUpdate', () => {
    ...
  });
    
  return () => adapty.removeAllListeners();
},[]);
```
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
Make sure to set up [URL for App Store Server Notifications](../../../settings/ios-sdk.md#app-store-connect-subscription-status-url) for iOS and [Real-time developer notifications \(RTDN\)](../../../settings/android-sdk.md#real-time-developer-notifications-rtdn) for Android to receive subscription updates without significant delays.
{% endhint %}

