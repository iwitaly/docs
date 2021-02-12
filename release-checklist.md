---
description: Steps to check before releasing the app with Adapty SDK
---

# Release Checklist

We’re thrilled you’ve decided to use Adapty! We want you to get the best results from the very first build. Here’s a quick overview of the steps needed for successful integration. Steps 1-4 are usually required, 5-7 are highly recommended;\)

1. Install Adapty SDK in your app. Make sure you use the **Public SDK key**. All SDK calls must be made after calling **`.activate()`** method. Otherwise, we won't be able to authenticate requests.
2. Fill in **App Store Connect shared secret** for [iOS](settings/ios-sdk.md#app-store-connect-shared-secret) and both **package name** and **service account key file** for [Android](settings/android-sdk.md#service-account-key-file). We need them to process purchases.
3. For iOS, update the **App Store Connect subscription status URL** with our [link](https://app.adapty.io/settings/ios-sdk). This way, we'll know about subscription events as soon as they occur. For Android, set up [real-time developer notifications \(RTDN\)](settings/android-sdk.md#real-time-developer-notifications-rtdn).
4. [Integrations](https://docs.adapty.io/analytics/integrations/3rd-party-analytics) require passing identifiers to our SDK. Amplitude, Mixpanel, Facebook Ads, and AppMetrica identifiers are passed using **`.updateProfile()`** method. AppsFlyer, Adjust, and Branch attribution data should be passed in **`.updateAttribution()`** method. Don't forget to configure specific integration in Adapty dashboard by providing API keys and event names.
5. For iOS, configure [App Store Connect API](https://app.adapty.io/settings/app-store-connect) integration to analyze historical data from App Store and get better predictions.
6. If you're willing to use promo campaigns, add [push certificates](https://app.adapty.io/settings/ios-sdk).
7. For iOS, if you use subscription offers, add a [subscription key](https://app.adapty.io/settings/ios-sdk), we'll use it to sign offers.

If you have any questions about integrating Adapty SDK, feel free to contact us at [support@adapty.io](mailto:support@adapty.io).

