---
description: >-
  Learn how to fetch and display products from paywalls in your app using Adapty
  Flutter SDK. With Adapty you can dynamically change the products visible to
  your users without new app releases
---

# Displaying Products

Adapty allows you to remotely configure the products that will be displayed in your app. This way you don't have to hardcode the products and can dynamically change offers or run A/B tests without app releases.

{% hint style="warning" %}
Make sure you've added the [products](../../../purchase-infrastructure/product.md) and [paywalls](../../../purchase-infrastructure/paywall.md) in Adapty Dashboard before fetching the products.
{% endhint %}

To fetch the products, you have to call **`.getPaywalls()`** method:

{% tabs %}
{% tab title="Flutter" %}
```dart
try {
	final GetPaywallsResult getPaywallsResult = await Adapty.getPaywalls(forceUpdate: Bool);
	final List<AdaptyPaywall> paywalls = getPaywallsResult.paywalls;
} on AdaptyError(adaptyError) {} 
catch(e) {}
```
{% endtab %}
{% endtabs %}

Request parameters:

* **Force update** \(optional\): a boolean indicating whether Adapty should fetch the data from API or get it from the local cache. Adapty SDK regularly refreshes the local data, so most of the time you don't have to use this flag. By default, it's set to `false`.

Response parameters:

* **Paywalls**: an array of **`AdaptyPaywall`** objects. This model contains the list of the products, paywall's identifier, custom payload, and several other properties. All you need to display the products in your app is to get a paywall by its identifier, retrieve the products, and display them.
* **Products**: an array of **`AdaptyProduct`** objects. This model contains product identifier, price, currency, title, and many other product options. Generally, you don't have to use this response parameter as all the products should be stored in the paywalls.

{% hint style="info" %}
Every time the data is fetched from a remote server, it will be stored in the local cache. This way, you can display the products even when the user is offline.
{% endhint %}

{% hint style="info" %}
Since the paywalls are configured remotely, the available products, the number of the products, and the special offers \(eg free trials\) can change over time. Make sure your code handles these scenarios. For example, if you get 2 products, the 2 products will be displayed, but when you get 3, all of them should be displayed without code changes.

**Don't hard code product ids**, you won't need them.
{% endhint %}



### Paywall analytics

{% hint style="warning" %}
By default, Adapty SDK sends**`paywallShow`** event which is accumulated in visitors metrics after every **`.getPaywalls()`** call. It works automatically, but it's incorrect because the user not necessarily was shown the paywall.

We strongly recommend disable automatic tracking and send these events manually for precise metric calculations.
{% endhint %}

First, disable automatic tracking by setting the flag **`AdaptyAutomaticPaywallsScreenReportingEnabled`** to **`false`** in **`Info.plist`** \(iOS\) and  **`AndroidManifest.xml`** \(Android\):

{% tabs %}
{% tab title="Info.plist" %}
```markup
<dict>
    ...
    <key>AdaptyAutomaticPaywallsScreenReportingEnabled</key>
    <false/>
</dict>
```
{% endtab %}

{% tab title="AndroidManifest.xml" %}
```markup
<application ...>
       ...
       <meta-data
              android:name="AdaptyAutomaticPaywallsScreenReportingEnabled"
              android:value="false" />
</application>
```
{% endtab %}
{% endtabs %}

Next, whenever you show a paywall to your user, call **`Adapty.logShowPaywall(paywall)`** to log **`paywallShow`** event related to your paywall.

