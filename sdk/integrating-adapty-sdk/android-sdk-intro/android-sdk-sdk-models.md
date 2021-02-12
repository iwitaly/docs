---
description: The models that are used in Adapty Android SDK
---

# SDK Models

### `ProductModel`

This model contains information about the product.

| Name | Type | Description |
| :--- | :--- | :--- |
| vendorProductId | str | Unique identifier of the product from Google Play. |
| localizedTitle | str | The title of the product for the user's localization. |
| localizedDescription | str | The description of the product ****for the user's localization. |
| localizedPrice | str | The formatted price of the product for the user's localization. |
| price | decimal | The price of the product in the user's local currency. |
| currencyCode | str | The ISO 4217 currency code for the user's localization \(USD, EUR\). |
| currencySymbol | str | The currency symbol for the user's localization. |
| subscriptionPeriod |  | A [**`ProductSubscriptionPeriodModel`**](android-sdk-sdk-models.md#productsubscriptionperiodmodel) object. The period details for products that are subscriptions. |
| introductoryOfferEligibility | bool | User's eligibility for the introductory offer. Check this property before displaying info about introductory offers, for example, free trials.  |
| promotionalOfferEligibility | bool | User's eligibility for the introductory offer. Check this property before displaying info about promotional offers. |
| introductoryDiscount |  | A [**`ProductDiscountModel`**](android-sdk-sdk-models.md#productdiscountmodel) object, containing introductory price information for the product. |
| skuDetails |  | [**`SkuDetails`**](https://developer.android.com/reference/com/android/billingclient/api/SkuDetails) assigned to this product. |
| paywallABTestName | str | Parent A/B test name |
| paywallName | str | Parent paywall name |



### **`ProductSubscriptionPeriodModel`**

| Name | Type | Description |
| :--- | :--- | :--- |
| unit | str | The unit of time that a subscription period is specified in. The possible values are: **`day`**, **`week`**, **`month`**, **`year`**. |
| numberOfUnits | int | The number of period units. |



### **`ProductDiscountModel`**

| Name | Type | Description |
| :--- | :--- | :--- |
| price | decimal | The discount price of the product in the user's local currency. |
| numberOfPeriods | int | An integer that indicates the number of periods the product discount is available. |
| localizedPrice | str | The formatted price of the discount for the user's localization. |
| subscriptionPeriod |  | A [**`ProductSubscriptionPeriodModel`**](android-sdk-sdk-models.md#productsubscriptionperiodmodel) object that defines the period for the product discount. |



### `PaywallModel`

This model contains information about the paywall including products.

| Name | Type | Description |
| :--- | :--- | :--- |
| developerId | str | The identifier of the paywall, configured in Adapty Dashboard. |
| variationId | str \(uuid\) | The identifier of the variation, used to attribute purchases to the paywall. |
| revision | int | The current revision \(version\) of the paywall. Every change within the paywall creates a new revision. |
| isPromo | bool | Whether this paywall is a part of the [Promo Campaign](../../../profiles-and-promo-campaigns/promo-campaigns.md). |
| customPayload | map | The custom JSON formatted data configured in Adapty Dashboard. |
| customPayloadString | str | The custom JSON formatted string configured in Adapty Dashboard. |
| products |  | A list of [**`ProductModel`**](android-sdk-sdk-models.md#productmodel) objects related to this paywall. |
| abTestName | str | Parent A/B test name |
| name | str | Paywall name |



### `PromoModel`

This model contains information about the promo offer for the user.

| Name | Type | Description |
| :--- | :--- | :--- |
| promoType | str | The type of the promo offer. |
| variationId | str \(uuid\) | The identifier of the variation, used to attribute purchases to the promo. |
| expiresAt | ISO 8601 datetime | The time when the current promo offer will expire. |
| paywall |  | A [**`PaywallModel`**](android-sdk-sdk-models.md#paywallmodel) object. |

\*\*\*\*

### **`PurchaserInfoModel`**

This model contains information about the user's subscription status and purchases history.

| Name | Type | Description |
| :--- | :--- | :--- |
| customerUserId | str | An identifier of the user in your system |
| accessLevels | map | The keys are access level identifiers configured by you in Adapty Dashboard. The values are [**`AccessLevelInfoModel`**](android-sdk-sdk-models.md#accesslevelinfomodel) objects. Can be null if the customer has no access levels. |
| subscriptions | map | The keys are product ids from Google Play. The values are [**`SubscriptionInfoModel`**](android-sdk-sdk-models.md#subscriptioninfomodel) objects. Can be null if the customer has no subscriptions. |
| nonSubscriptions | map | The keys are product ids from Google Play. The values are list\[\] of [**`NonSubscriptionInfoModel`**](android-sdk-sdk-models.md#nonsubscriptioninfomodel) objects. Can be null if the customer has no purchases. |



### **`AccessLevelInfoModel`**

This model contains information about the user's access level.

| Name | Type | Description |
| :--- | :--- | :--- |
| id | str | Unique identifier of the access level configured by you in Adapty Dashboard. |
| isActive | bool | Whether the access level is active. Generally, you have to check just this property to determine if the user has access to premium features.  |
| vendorProductId | str | The identifier of the product in Google Play that unlocked this access level. |
| vendorTransactionId | str | Transaction id of the purchase that unlocked this access level. |
| vendorOriginalTransactionId | str | Original transaction id of the purchase that unlocked this access level. For auto-renewable subscription, this will be the id of the first transaction in the subscription. |
| store | str | The store of the purchase that unlocked this access level. The possible values are: **`app_store`**, **`play_store`** , **`adapty`**. |
| activatedAt | ISO 8601 datetime | The time when the access level was activated. |
| startsAt | ISO 8601 datetime | The time when the access level has started \(could be in the future\). |
| renewedAt | ISO 8601 datetime | The time when the access level was renewed. |
| expiresAt | ISO 8601 datetime | The time when the access level will expire \(could be in the past and could be null for lifetime access\). |
| isLifetime | bool | Whether the access level is active for a lifetime \(no expiration date\). If set to true you shouldn't check **`expires_at`** , or you could just check **`isActive`**. |
| willRenew | bool | Whether the auto-renewable subscription is set to renew. |
| isInGracePeriod | bool | Whether the auto-renewable subscription is in the [grace period](https://help.apple.com/app-store-connect/#/dev58bda3212). |
| unsubscribedAt | ISO 8601 datetime | The time when the auto-renewable subscription was cancelled. Subscription can still be active, it just means that auto-renewal turned off. Will be set to null if the user reactivates the subscription. |
| billingIssueDetectedAt | ISO 8601 datetime | The time when billing issue was detected \(Google was not able to charge the card\). Subscription can still be active. Will be set to null if the charge will be made. |
| cancellation\_reason | str | The reason why the subscription was cancelled. Possible values are: **`voluntarily_cancelled`**, **`billing_error`**, **`refund`**, **`price_increase`**, **`product_was_not_available`**, **`unknown`**. |
| is\_refund | bool | Whether the purchase was refunded. |
| activeIntroductoryOfferType | str | The type of active introductory offer. Possible values are: **`free_trial`**, **`pay_as_you_go`,** **`pay_up_front`**. If the value is not null, it means that the offer was applied during the current subscription period. |
| activePromotionalOfferType | str | The type of active promotional offer. Possible values are: **`free_trial`**, **`pay_as_you_go`,** **`pay_up_front`**. If the value is not null, it means that the offer was applied during the current subscription period. |



### **`SubscriptionInfoModel`**

This model contains information about the user's subscription.

| Name | Type | Description |
| :--- | :--- | :--- |
| isActive | bool | Whether the subscription is active. |
| vendorProductId | str | The identifier of the product in Google Play. |
| vendorTransactionId | str | Transaction id from Google Play. |
| vendorOriginalTransactionId | str | Original transaction id from Google Play. For auto-renewable subscription, this will be the id of the first transaction in the subscription. |
| store | str | The store of the purchase. The possible values are: **`app_store`**, **`play_store`** , **`adapty`**. |
| activatedAt | ISO 8601 datetime | The time when the subscription was activated. |
| startsAt | ISO 8601 datetime | The time when the subscription has started \(could be in the future\). |
| renewedAt | ISO 8601 datetime | The time when the subscription was renewed. |
| expiresAt | ISO 8601 datetime | The time when the subscription will expire \(could be in the past and could be null for lifetime access\). |
| isLifetime | bool | Whether the subscription is active for a lifetime \(no expiration date\). If set to true you shouldn't check **`expires_at`** , or you could just check **`isActive`**. |
| willRenew | bool | Whether the auto-renewable subscription is set to renew. |
| isInGracePeriod | bool | Whether the auto-renewable subscription is in the [grace period](https://help.apple.com/app-store-connect/#/dev58bda3212). |
| unsubscribedAt | ISO 8601 datetime | The time when the auto-renewable subscription was cancelled. Subscription can still be active, it just means that auto-renewal turned off. Will be set to null if the user reactivates the subscription. |
| billingIssueDetectedAt | ISO 8601 datetime | The time when billing issue was detected \(Google was not able to charge the card\). Subscription can still be active. Will be set to null if the charge will be made. |
| cancellation\_reason | str | The reason why the subscription was cancelled. Possible values are: **`voluntarily_cancelled`**, **`billing_error`**, **`refund`**, **`price_increase`**, **`product_was_not_available`**, **`unknown`**. |
| is\_refund | bool | Whether the purchase was refunded. |
| activeIntroductoryOfferType | str | The type of active introductory offer. Possible values are: **`free_trial`**, **`pay_as_you_go`,** **`pay_up_front`**. If the value is not null, it means that the offer was applied during the current subscription period. |
| activePromotionalOfferType | str | The type of active promotional offer. Possible values are: **`free_trial`**, **`pay_as_you_go`,** **`pay_up_front`**. If the value is not null, it means that the offer was applied during the current subscription period. |
| isSandbox | bool | Whether the product was purchased in the sandbox environment. |



### **`NonSubscriptionInfoModel`**

This model contains information about the user's non-subscription purchases.

| Name | Type | Description |
| :--- | :--- | :--- |
| purchaseId | str | The identifier of the purchase in Adapty. You can use it to ensure that you've already processed this purchase \(for example tracking one time products\). |
| vendorProductId | str | The identifier of the product in Google Play. |
| vendorTransactionId | str | Transaction id from Google Play. |
| store | str | The store of the purchase. The possible values are: **`app_store`**, **`play_store`** , **`adapty`**. |
| purchasedAt | ISO 8601 datetime | The time when the product was purchased. |
| is\_refund | bool | Whether the purchase was refunded. |
| isOneTime | bool | Whether the product should only be processed once. If true, the purchase will be returned by Adapty API one time only. |
| isSandbox | bool | Whether the product was purchased in the sandbox environment. |

