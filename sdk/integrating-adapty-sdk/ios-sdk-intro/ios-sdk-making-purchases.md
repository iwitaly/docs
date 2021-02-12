---
description: >-
  Learn how to make and restore mobile purchases using Adapty iOS SDK. Adapty
  handles server-side validation, including renewals and grace periods
---

# Making Purchases

To make the purchase, you have to call **`.makePurchase()`** method:

{% tabs %}
{% tab title="Swift" %}
```swift
Adapty.makePurchase(product: <product>, offerId: <offerId>) { (purchaserInfo, receipt, appleValidationResult, product, error) in
    if error == nil {
        // successful purchase
    }
}
```
{% endtab %}
{% endtabs %}

Request parameters:

* **Product** \(required\): a [**`ProductModel`**](ios-sdk-models.md#productmodel) object retrieved from the paywall.
* **Offer Id** \(optional\): a string identifier of promotional offer from App Store Connect. Adapty signs the request according to Apple guidelines, please make sure you've uploaded [Subscription Key](../../../settings/ios-sdk.md#subscription-key) in Adapty Dashboard when using promotional offers.

Response parameters:

* **Purchaser info**: a [**`PurchaserInfoModel`**](ios-sdk-models.md#purchaserinfomodel) object. This model contains info about access levels, subscriptions, and non-subscription purchases. Generally, you have to check only access level status to determine whether the user has premium access to the app.
* **Receipt**: a string representation of Apple's receipt.
* **Apple validation result**: a dictionary containing [raw validation result](https://developer.apple.com/documentation/appstorereceipts/responsebody) from Apple.
* **Product**: a [**`ProductModel`**](ios-sdk-models.md#productmodel) object you've passed to this method.

{% hint style="warning" %}
Make sure you've added [App Store Connect shared secret](../../../settings/ios-sdk.md#app-store-connect-shared-secret) in Adapty Dashboard, without it, we can't validate purchases.
{% endhint %}

Below is a complete example of making the purchase and checking the user's access level.

{% tabs %}
{% tab title="Swift" %}
```swift
Adapty.makePurchase(product: <product>, offerId: <offerId>) { (purchaserInfo, receipt, appleValidationResult, product, error) in
    if error == nil {
        // "premium" is an identifier of default access level
        if purchaserInfo?.accessLevels["premium"]?.isActive == true {
            // grant access to premium features
        }
    }
}
```
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
Make sure to set up [URL for App Store Server Notifications](../../../settings/ios-sdk.md#app-store-connect-subscription-status-url) to receive subscription updates without significant delays.
{% endhint %}



### Restoring purchases

To restore purchases, you have to call **`.restorePurchases()`** method:

{% tabs %}
{% tab title="Swift" %}
```swift
Adapty.restorePurchases { (purchaserInfo, receipt, appleValidationResult, error) in
    if error == nil {
        // successful restore
    }
}
```
{% endtab %}
{% endtabs %}

Response parameters:

* **Purchaser info**: a [**`PurchaserInfoModel`**](ios-sdk-models.md#purchaserinfomodel) object. This model contains info about access levels, subscriptions, and non-subscription purchases. Generally, you have to check only access level status to determine whether the user has premium access to the app.
* **Receipt**: a string representation of Apple's receipt.
* **Apple validation result**: a dictionary containing [raw validation result](https://developer.apple.com/documentation/appstorereceipts/responsebody) from Apple.



### Receipt validation

If you want to validate the existing receipt, you should call **`.validateReceipt()`** method:

{% tabs %}
{% tab title="Swift" %}
```swift
Adapty.validateReceipt("<receiptEncoded>") { (purchaserInfo, appleValidationResult, error) in
    if error == nil {
        // successful validation
    }
}
```
{% endtab %}
{% endtabs %}

Request parameters:

* **Receipt encoded** \(required\): a string representation of Apple's receipt.

Response parameters:

* **Purchaser info**: a [**`PurchaserInfoModel`**](ios-sdk-models.md#purchaserinfomodel) object. This model contains info about access levels, subscriptions, and non-subscription purchases. Generally, you have to check only access level status to determine whether the user has premium access to the app.
* **Apple validation result**: a dictionary containing [raw validation result](https://developer.apple.com/documentation/appstorereceipts/responsebody) from Apple.



### Deferred purchases

For deferred purchases, Adapty SDK has an optional delegate method, which is called when the user starts the purchase in the App Store, and the transaction continues in your app. Just store **`makeDeferredPurchase`** and call it later if you want to hold your purchase for now. Then show the paywall to your user. To continue purchase, call **`makeDeferredPurchase`**.

{% tabs %}
{% tab title="Swift" %}
```swift
extension AppDelegate: AdaptyDelegate {

    func paymentQueue(shouldAddStorePaymentFor product: ProductModel, defermentCompletion makeDeferredPurchase: @escaping DeferredPurchaseCompletion) {
        // you can store makeDeferredPurchase callback and call it later
        
        // or you can call it right away
        makeDeferredPurchase { (purchaserInfo, receipt, appleValidationResult, product, error) in
            // check the purchase
        }
    }
    
}
```
{% endtab %}
{% endtabs %}

