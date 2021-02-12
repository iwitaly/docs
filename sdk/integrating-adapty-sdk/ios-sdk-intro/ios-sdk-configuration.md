---
description: >-
  Learn how to import Adapty iOS SDK in your app, configure it, and set up
  debugging
---

# Configuration

In your **`AppDelegate`** class:

{% tabs %}
{% tab title="Swift" %}
```swift
import Adapty
```
{% endtab %}
{% endtabs %}

And add the following to **`application(_:didFinishLaunchingWithOptions:)`**:

{% tabs %}
{% tab title="Swift" %}
```swift
Adapty.activate("PUBLIC_SDK_KEY", customerUserId: "YOUR_USER_ID")
```
{% endtab %}
{% endtabs %}

Adapty configurational options:

* **Public SDK key** \(required\): found in your app settings in [Adapty Dashboard](https://app.adapty.io/settings/general) `App settings` &gt; `General`. 
* **Customer user ID** \(optional\): an identifier of the user in your system. We send it in subscription and analytical [events](../../../analytics/integrations/events.md), to attribute events to the right profile. You can also find customers by **`customerUserId`** in the [Profiles](../../../profiles-and-promo-campaigns/profiles.md) section. If you don't have user IDs in your app, you can omit this parameter or pass null. If you don't have a user ID at the time of Adapty initialization, you can set it later using **`.identify()`** method. Read more in the [Identifying Users](ios-sdk-identifying-users.md#setting-customer-user-id-after-configuration) section.
* **Observer mode** \(optional\): a boolean value controlling [Observer mode](ios-sdk-observer-mode.md). Turn it on if you handle purchases and subscription status yourself and use Adapty for sending subscription events and analytics.

{% hint style="warning" %}
Make sure you use the **Public SDK key** for Adapty initialization, the **Secret key** should be used for [server-side API](../../../server-side-api/getting-started.md) only.
{% endhint %}

{% hint style="info" %}
**SDK keys** are unique for every app, so if you have multiple apps make sure you choose the right one.
{% endhint %}



### Debugging

Adapty logs errors and other important information to help you understand what is going on. There are three levels available:

1. **`.none`** \(default\): won't log anything
2. **`.errors`**: only errors will be logged 
3. **`.verbose`**: method invocations, API requests/responses, and errors will be logged

You can set **`logLevel`** in your app before configuring Adapty.

{% tabs %}
{% tab title="Swift" %}
```swift
Adapty.logLevel = .verbose
```
{% endtab %}
{% endtabs %}

