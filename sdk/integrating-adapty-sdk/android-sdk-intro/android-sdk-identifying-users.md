---
description: >-
  Learn how to identify users of your app using Adapty Android SDK. Identified
  users have access to subscriptions across all available platforms: Android,
  iOS, web
---

# Identifying Users

Adapty creates an internal profile id for every user. But if you have your authentification system you should set your own Customer User Id. You can find the users by Customer User Id in [Adapty Dashboard](https://docs.adapty.io/profiles-and-promo-campaigns/profiles), use it in [server-side API](https://docs.adapty.io/server-side-api/getting-started), it will be sent to all [integrations](https://docs.adapty.io/analytics/integrations/3rd-party-analytics) and [webhook](https://docs.adapty.io/analytics/integrations/webhook).

​

### Setting customer user Id on configuration <a id="setting-customer-user-id-on-configuration"></a>

If you have a user id during configuration, just pass it as **`customerUserId`** parameter to **`.activate()`** method:

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
Adapty.activate(applicationContext, "PUBLIC_SDK_KEY", customerUserId: "YOUR_USER_ID")
```
{% endtab %}
{% endtabs %}

​

### Setting customer user Id after configuration <a id="setting-customer-user-id-after-configuration"></a>

If you don't have a user id on SDK configuration, you can set it later at any time with **`.identify()`** method. The most common cases are after registration/authorization when the user switches from being an anonymous user to an authenticated user.

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
Adapty.identify("YOUR_USER_ID") { error ->
    if (error == null) {
        // successful identify
    }
}
```
{% endtab %}
{% endtabs %}

Request parameters:

* **User Id** \(required\): a string user identifier.



### Logging out and logging in <a id="logging-out-and-logging-in"></a>

You can logout the user anytime by calling **`.logout()`** method:

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
Adapty.logout { error ->
    if (error == null) {
        // successful logout
    }
}
```
{% endtab %}
{% endtabs %}

You can then login the user using **`.identify()`** method.

