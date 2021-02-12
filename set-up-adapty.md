# Set up Adapty

### **Try Adapty without coding or install SDK with a single line of code**

You can integrate Adapty in three different ways.

1. **Starter mode**. Upload your [App Store Connect credentials](settings/app-store-connect.md) and get immediate access to Basic Analytics. It's free forever and takes under 5 minutes.
2. **Observer mode**. Adapty will get data from the transactions queue and analyze them. Use your existing payment processing.
3. **Full mode**. Use Adapty for payment processing \(server-side receipt verification\), [A/B tests](purchase-infrastructure/ab-tests.md), [Promo Campaigns](profiles-and-promo-campaigns/promo-campaigns.md), and more.

For Observer and Full mode, it's required to install [Adapty SDK](sdk/integrating-adapty-sdk/). 

Observer mode is made for developers with complex legacy subscription infrastructure. Full mode extends Observer with remotely configured A/B tests for products. Starter mode is free forever, Observer and Management modes have the same [pricing](https://adapty.io/pricing.html).

{% hint style="info" %}
Adapty does not replace payment processing from Apple/Google. In Full mode, Adapty handles [subscription billing](https://developer.apple.com/documentation/storekit/in-app_purchase/subscriptions_and_offers/handling_subscriptions_billing) without implementing server logic on your side.
{% endhint %}

Compare how different integrations unlock different features.

| Feature | Starter | Observer | Full |
| :--- | :--- | :--- | :--- |
| **Unlimited apps** | ✅ | ✅ | ✅ |
| **Unlimited users** | ✅ | ✅ | ✅ |
| **Basic analytics** | ✅ | ✅ | ✅ |
| **Advanced analytics** | ➖ | ✅ | ✅ |
| **Promo campaigns** | ➖ | ✅ | ✅ |
| **Integrations** | ➖ | ✅ | ✅ |
| **Subscribers CRM** | ➖ | ✅ | ✅ |
| **Server-side receipt verification** | ➖ | ➖ | ✅ |
| **A/B tests for products** | ➖ | ➖ | ✅ |

