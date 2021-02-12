---
description: >-
  Learn how to use Adapty iOS SDK in Observer mode along with existing purchase
  infrastructure
---

# Observer Mode

If you have a functioning subscription system and want to give Adapty SDK a quick try, you can use Observer mode. With just one line of code you can:

* get insights by using our top-class [analytics](../../../analytics/advanced-analytics.md);
* send subscription [events](../../../analytics/integrations/events.md) to your [server](../../../analytics/integrations/webhook.md) and [3rd party services](../../../analytics/integrations/3rd-party-analytics.md);
* view and analyze customers in Adapty [CRM](../../../profiles-and-promo-campaigns/profiles.md).

Adapty SDK will automatically collect all transactions and will be sending subscription events. To turn on Observer mode, just set **`observerMode`** to **`true`** when activating Adapty:

{% tabs %}
{% tab title="Swift" %}
```swift
Adapty.activate("PUBLIC_SDK_KEY", customerUserId: "YOUR_USER_ID", observerMode: true)
```
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
When running in Observer mode, Adapty SDK won't close any transactions, so make sure you're handling it.
{% endhint %}



### A/B tests analytics

In Observer mode, Adapty SDK doesn't know, where the purchase was made from. If you display products using our [Paywalls](../../../purchase-infrastructure/paywall.md) or [A/B tests](../../../purchase-infrastructure/ab-tests.md), you can manually assign variation to the purchase. After doing this, you'll be able to see metrics in Adapty Dashboard.

```swift
let transactionId = transaction.transactionIdentifier
let variationId = paywall.variationId

Adapty.setVariationId(variationId, forTransactionId: transactionId) { (error) in
    if error == nil {
        // successful binding
    }
}
```

Request parameters:

* **Variation Id** \(required\): a string identifier of variation. You can get it using **`variationId`** property of [**`PaywallModel`**](ios-sdk-models.md#paywallmodel).
* **Transaction Id** \(required\): a string identifier \(**`transactionIdentifier`**\) of your purchased transaction [**`SKPaymentTransaction`**](https://developer.apple.com/documentation/storekit/skpaymenttransaction).

