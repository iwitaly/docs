---
description: Learn how to install Adapty iOS SDK via CocoaPods or Swift Package Manager
---

# Installation

You can install Adapty SDK via [CocoaPods](ios-sdk-installation.md#install-via-cocoapods), or [Swift Package Manager](ios-sdk-installation.md#install-via-swift-package-manager).

{% hint style="info" %}
Make sure to set Swift 5.0+ for Adapty pod in case your app is using the older version.
{% endhint %}

### Install via CocoaPods

Add Adapty to your **`Podfile`**:

{% code title="Podfile" %}
```bash
pod 'Adapty', '~> 1.12.2'
```
{% endcode %}

And then run:

```bash
pod install
```

This creates an **`.xcworkspace`** file for your app. Use this file for all future development of your application.



### Install via Swift Package Manager

1. In Xcode go to `File` &gt; `Swift Packages` &gt; `Add Package Dependency...`
2. Enter the repository URL `https://github.com/adaptyteam/AdaptySDK-iOS.git`
3. Choose the version, and click `Next`. Xcode will add the package dependency to your project, and you can import it.

