---
description: >-
  Learn how to set user attributes using Adapty Android SDK. You can then use
  attributes to segment profiles
---

# Setting User Attributes

You can set optional attributes such as email, phone number, etc, to the user of your app. You can then use attributes to create user [segments](../../../profiles-and-promo-campaigns/segments.md) or just view them in CRM.

To set user attributes, call **`.updateProfile()`** method:

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
val params = ProfileParameterBuilder()
    .withEmail("email@example.com")
    .withBirthday(Date(1970, 1, 3))
    .withCustomAttributes(mapOf("key1" to value1, "key2" to value2))
    ...with<Key>(<Value>)

Adapty.updateProfile(params) { error ->
    if error == null {
        // successful update                              
    }
}
```
{% endtab %}
{% endtabs %}

The allowed keys **`<Key>`** of **`ProfileParameterBuilder()`** and the values **`<Value>`** are listed below:

| **&lt;Key&gt;** | **&lt;Value&gt;** |
| :--- | :--- |
| email | String up to 30 characters |
| phoneNumber | String up to 15 characters |
| facebookUserId | String up to 30 characters |
| amplitudeUserId | String up to 30 characters |
| amplitudeDeviceId | String up to 30 characters |
| mixpanelUserId | String up to 30 characters |
| appmetricaProfileId | String up to 30 characters |
| appmetricaDeviceId | String up to 30 characters |
| firstName | String up to 30 characters |
| lastName | String up to 30 characters |
| gender | Enum, allowed values are: **`female`**, **`male`**, **`other`** |
| birthday | Date |
| customAttributes | Dictionary, read more in the [Custom User Attributes](android-sdk-setting-user-attributes.md#custom-user-attributes) section. |



### Custom user attributes

You can set your own custom attributes. These are usually related to your app usage. For example, for fitness applications, they might be the number of training per week, for language learning app user's knowledge level, and so on. You can use them in segments to create targeted paywalls and offers, and you can also use them in analytics to figure out which product metrics affect the revenue most.

You can set up to 10 custom attributes for the user, the attribute's key and value should be up to 30 characters. The keys can be only strings of letters, numbers, dashes, points, and underscores. The values can be both strings and numbers. Boolean values will be converted to integers.

Contact us if you need higher limits for custom user attributes.

