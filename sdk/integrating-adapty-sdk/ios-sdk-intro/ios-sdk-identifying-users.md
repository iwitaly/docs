---
description: >-
  Learn how to identify users of your app using Adapty iOS SDK. Identified users
  have access to subscriptions across all available platforms: iOS, Android, web
---

# Identifying Users

Adapty creates an internal profile id for every user. But if you have your authentification system you should set your own Customer User Id. You can find the users by Customer User Id in [Adapty Dashboard](../../../profiles-and-promo-campaigns/profiles.md), use it in [server-side API](../../../server-side-api/getting-started.md), it will be sent to all [integrations](../../../analytics/integrations/3rd-party-analytics.md) and [webhook](../../../analytics/integrations/webhook.md).



### Setting customer User Id on configuration

If you have a user id during configuration, just pass it as **`customerUserId`** parameter to **`.activate()`** method:

{% tabs %}
{% tab title="Swift" %}
```swift
Adapty.activate("PUBLIC_SDK_KEY", customerUserId: "YOUR_USER_ID")
```
{% endtab %}
{% endtabs %}



### Setting customer user Id after configuration

If you don't have a user id on SDK configuration, you can set it later at any time with **`.identify()`** method. The most common cases are after registration/authorization when the user switches from being an anonymous user to an authenticated user.

{% tabs %}
{% tab title="Swift" %}
```swift
Adapty.identify("YOUR_USER_ID") { (error) in
    if error == nil {
        // successful identify
    }
}
```
{% endtab %}
{% endtabs %}

Request parameters:

* **User Id** \(required\): a string user identifier.



### Logging out and logging in

You can logout the user anytime by calling **`.logout()`** method:

{% tabs %}
{% tab title="Swift" %}
```swift
Adapty.logout { (error) in
    if error == nil {
        // successful logout
    }
}
```
{% endtab %}
{% endtabs %}

You can then login the user using **`.identify()`** method.

