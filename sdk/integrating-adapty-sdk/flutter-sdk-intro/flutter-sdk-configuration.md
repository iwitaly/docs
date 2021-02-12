---
description: >-
  Learn how to import Adapty Flutter SDK in your app, configure it, and set up
  debugging
---

# Configuration

First, add the flag **`AdaptyPublicSdkKey`** in the app’s **`Info.plist`** \(iOS\) and **`AndroidManifest.xml`** \(Android\) file with the value of your Public SDK key. It can be found in your app settings in [Adapty Dashboard](https://app.adapty.io/settings/general) `App settings` &gt; `General`.

{% tabs %}
{% tab title="Info.plist" %}
```markup
<dict>
    ...
    <key>AdaptyPublicSdkKey</key>
    <string>PUBLIC_SDK_KEY</string>
</dict>
```
{% endtab %}

{% tab title="AndroidManifest.xml" %}
```markup
<application ...>
       ...
       <meta-data
              android:name="AdaptyPublicSdkKey"
              android:value="PUBLIC_SDK_KEY" />
</application>
```
{% endtab %}
{% endtabs %}

For iOS, you can optionally set the flag **`AdaptyObserverMode`** to **`true`** , if you want Adapty to run in Observer mode. Usually, it means, that you handle purchases and subscription status yourself and use Adapty for sending subscription events and analytics.

Then in your application:

{% tabs %}
{% tab title="Flutter" %}
```dart
import 'package:adapty_flutter/adapty_flutter.dart';
```
{% endtab %}
{% endtabs %}

And finally, activate Adapty SDK with the following code :

{% tabs %}
{% tab title="Flutter" %}
```dart
Adapty.activate();
```
{% endtab %}
{% endtabs %}

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
{% tab title="Flutter" %}
```dart
try {
	await Adapty.setLogLevel(AdaptyLogLevel.verbose);
} on AdaptyError catch (adaptyError) {}
catch (e) {}
```
{% endtab %}
{% endtabs %}

