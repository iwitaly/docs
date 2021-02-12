---
description: >-
  Learn how to fetch and display products from paywalls in your app using Adapty
  iOS SDK. With Adapty you can dynamically change the products visible to your
  users without new app releases
---

# Displaying Products

Adapty allows you to remotely configure the products that will be displayed in your app. This way you don't have to hardcode the products and can dynamically change offers or run A/B tests without app releases.

{% hint style="warning" %}
Make sure you've added the [products](../../../purchase-infrastructure/product.md) and [paywalls](../../../purchase-infrastructure/paywall.md) in Adapty Dashboard before fetching the products.
{% endhint %}

To fetch the products, you have to call **`.getPaywalls()`** method:

{% tabs %}
{% tab title="Swift" %}
```swift
Adapty.getPaywalls(forceUpdate: Bool) { (paywalls, products, error) in
    if error == nil {
        // retrieve the products from paywalls
    }
}
```
{% endtab %}
{% endtabs %}

Request parameters:

* **Force update** \(optional\): a boolean indicating whether Adapty should fetch the data from API or get it from the local cache. Adapty SDK regularly refreshes the local data, so most of the time you don't have to use this flag. By default, it's set to `false`.

Response parameters:

* **Paywalls**: an array of [**`PaywallModel`**](ios-sdk-models.md#paywallmodel) objects. This model contains the list of the products, paywall's identifier, custom payload, and several other properties. All you need to display the products in your app is to get a paywall by its identifier, retrieve the products, and display them.
* **Products**: an array of [**`ProductModel`**](ios-sdk-models.md#productmodel) objects. This model contains product identifier, price, currency, title, and many other product options. Generally, you don't have to use this response parameter as all the products should be stored in the paywalls.

{% hint style="info" %}
Every time the data is fetched from a remote server, it will be stored in the local cache. This way, you can display the products even when the user is offline.
{% endhint %}

{% hint style="warning" %}
Since the paywalls are configured remotely, the available products, the number of the products, and the special offers \(eg free trials\) can change over time. Make sure your code handles these scenarios. For example, if you get 2 products, the 2 products will be displayed, but when you get 3, all of them should be displayed without code changes.  
  
**Don't hard code product ids**, you won't need them.
{% endhint %}



### Showcase

First, get the paywall you need using an ID from Adapty Dashboard:

{% tabs %}
{% tab title="Swift" %}
```swift
var paywall: PaywallModel?
Adapty.getPaywalls { (paywalls, _, error) in
    paywall = paywalls?.first(where: { $0.developerId == "your_paywall_id" })
}
```
{% endtab %}
{% endtabs %}

Next, build your paywall view using **`paywall.products`** and show it to the user. Later on, when the user makes a purchase, simply call **`.makePurchase()`** with the product from your paywall.

{% tabs %}
{% tab title="Swift" %}
```swift
let product = paywall?.products.first

Adapty.makePurchase(product: product) { (purchaserInfo, receipt, appleValidationResult, product, error) in
    if error == nil {
        // successful purchase
    }
}
```
{% endtab %}
{% endtabs %}



### Paywall analytics

Adapty helps you to measure the performance of the paywalls. We automatically collect all the [metrics](../../../purchase-infrastructure/paywall.md#metrics) related to purchases except for paywall views. This is because only you know when the paywall was shown to a customer.

Whenever you show a paywall to your user, call **`.logShowPaywall(paywall)`** to log the event, and it will be accumulated in the paywall metrics.

{% tabs %}
{% tab title="Swift" %}
```swift
Adapty.logShowPaywall(paywall)
```
{% endtab %}
{% endtabs %}

Request parameters:

* **Paywall** \(required\): a [**`PaywallModel`**](ios-sdk-models.md#paywallmodel) object.



### Fallback paywalls

Adapty allows you to provide fallback paywalls that will be used when a user opens the app for the first time and there's no internet connection. Or in the rare case when Adapty backend is down and there's no cache on the device.

To set fallback paywalls, use **`.setFallbackPaywalls(paywalls)`** method. You should pass exactly the same payload you're getting from Adapty backend. You can either copy it from the real response or contact us so we can provide it for you. We will add the ability to copy fallback paywall data from Adapty Dashboard. 

Here's an example of getting fallback paywall data from the locally stored JSON file named **`fallback_paywalls`**.

{% tabs %}
{% tab title="Swift" %}
```swift
if let path = Bundle.main.path(forResource: "fallback_paywalls", ofType: "json"), let paywalls = try? String(contentsOfFile: path, encoding: .utf8) {
    // you can get paywalls string any other way as well
    Adapty.setFallbackPaywalls(paywalls)
}
```
{% endtab %}
{% endtabs %}

Request parameters:

* **Paywalls** \(required\): a JSON representation of your paywalls/products list in the exact same format as provided by Adapty backend.

{% hint style="info" %}
You can also hardcode fallback paywall data or receive it from your remote server.
{% endhint %}

