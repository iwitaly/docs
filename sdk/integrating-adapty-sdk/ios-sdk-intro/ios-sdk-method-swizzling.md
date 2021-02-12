---
description: Learn how to manually set push tokens using Adapty iOS SDK
---

# Method Swizzling

Adapty SDK performs method swizzling to receive APNs tokens. Developers, who prefer not to use swizzling, can disable it by adding the flag **`AdaptyAppDelegateProxyEnabled`** in the app’s **`Info.plist`** file and set it to **`NO`** \(boolean value\).

If you have disabled method swizzling, you'll need to explicitly send your APNs to Adapty. Override the method **`didRegisterForRemoteNotificationsWithDeviceToken`** to retrieve the APNs token, and then set Adapty's **`apnsToken`** property:

{% tabs %}
{% tab title="Swift" %}
```swift
func application(application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: NSData) {
    Adapty.apnsToken = deviceToken
}
```
{% endtab %}
{% endtabs %}

