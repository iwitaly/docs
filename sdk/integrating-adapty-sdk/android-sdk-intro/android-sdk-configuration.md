---
description: >-
  Learn how to import Adapty Android SDK in your app, configure it, and set up
  logging
---

# Configuration

Add the following to your **`Application`** class:

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
override fun onCreate() {
    super.onCreate()
    Adapty.activate(applicationContext, "PUBLIC_SDK_KEY", customerUserId: "YOUR_USER_ID")
}
```
{% endtab %}
{% endtabs %}

Adapty configurational options:

* **Public SDK key** \(required\): found in your app settings in [Adapty Dashboard](https://app.adapty.io/settings/general) `App settings` &gt; `General`. 
* **Customer user ID** \(optional\): an identifier of the user in your system. We send it in subscription and analytical [events](../../../analytics/integrations/events.md), to attribute events to the right profile. You can also find customers by **`customerUserId`** in the [Profiles](../../../profiles-and-promo-campaigns/profiles.md) section. If you don't have user IDs in your app, you can omit this parameter or pass null. If you don't have a user ID at the time of Adapty initialization, you can set it later using **`.identify()`** method. Read more in the [Identifying Users](android-sdk-identifying-users.md#setting-customer-user-id-after-configuration) section.

{% hint style="warning" %}
Make sure you use the **Public SDK key** for Adapty initialization, the **Secret key** should be used for [server-side API](../../../server-side-api/getting-started.md) only.
{% endhint %}

{% hint style="info" %}
**SDK keys** are unique for every app, so if you have multiple apps make sure you choose the right one.
{% endhint %}



### Logging

Adapty logs errors and other important information to help you understand what is going on. There are three levels available:

1. **`AdaptyLogLevel.NONE`** \(default\): won't log anything
2. **`AdaptyLogLevel.ERROR`**: only errors will be logged 
3. **`AdaptyLogLevel.VERBOSE`**: method invocations, API requests/responses, and errors will be logged

You can set the log level in your app before configuring Adapty.

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
Adapty.setLogLevel(AdaptyLogLevel.VERBOSE)
```
{% endtab %}
{% endtabs %}

