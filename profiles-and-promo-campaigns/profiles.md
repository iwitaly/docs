---
description: Manage subscriptions and analyze events for each user
---

# Profiles/CRM

Profiles is a CRM for your users. With Profiles you can:

1. Find a user with any ID you have including email and phone number
2. Explore the full payment path of a user including billing issues, grace periods, and other [events](../analytics/integrations/#events)
3. Analyze users properties such as subscription state, total revenue/proceeds, last seen, and more 
4. Grant user a subscription

![](../.gitbook/assets/profiles.png)

In a full table of subscribers, you can filter, sort, and find users. The state describes user state in terms of a subscription and can be:

* **Subscribed**. A user has an active subscription
* **Active trial**. A user has a subscription with an active trial period
* **Auto renew off**. A user turned off auto-renewal. Check [events](../analytics/integrations/#events) for more info
* **Subscription cancelled**. A user cancelled a subscription. Check [events](../analytics/integrations/#events) for more info
* **Trial cancelled**. A user cancelled a trial
* **Never subscribed**. A user has never subscribed, i.e. he's a freemium user
* **Billing issue**. A user is can't be charged
* **Grace period**. A user entered a grace period

You can group users into Segment to make [promo campaigns](promo-campaigns.md), group analysis, and more.

{% page-ref page="segments.md" %}



### Users properties

![](../.gitbook/assets/profile-1.jpg)

You can send any properties that you want for the user. Find in [iOS SDK](https://github.com/adaptyteam/AdaptySDK-iOS) how to do it.

By default Adapty set

* **App User ID**. Is a developer ID and can be any string
* **Adapty ID**. Internal ID of a user in Adapty
* **IDFA**
* **Country**
* **OS**
* **Device**
* **Created at**. Profile creation date
* **Last seen**

For a better understanding, your user we suggest sending at least your internal user ID or user email. This will help you to find a user.

After installing [Adapty SDK](https://github.com/adaptyteam/AdaptySDK-iOS) Adapty automatically collect user [events](../analytics/integrations/#events) from the payment queue and display them in a user profile.



### Custom attributes

You can see custom attributes that were set either from [SDK](https://github.com/adaptyteam/AdaptySDK-iOS/blob/master/Documentation/AdvancedUsage.md#update-your-user-attributes) and manually assign them to the user using the Add attribute button in the Attributes section on the profile page.

![](../.gitbook/assets/image%20%2870%29.png)

### 

### Grant a subscription

In a profile, you can find an active subscription. At any time you can prolong the user's subscription or grant lifetime access. 

![Changing paid access level](../.gitbook/assets/image%20%2830%29.png)

It's most useful for users without an active subscription so you can grant the individual user or a group of users premium features for some time.

{% hint style="info" %}
Expires at must be a date in the future and ones set it can't be decreased
{% endhint %}



