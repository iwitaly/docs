---
description: >-
  Configure iOS SDK to validate purchases, get subscription updates, and send
  push notifications
---

# iOS SDK

For [Adapty iOS SDK](https://github.com/adaptyteam/AdaptySDK-iOS) to work you need to enter a couple of keys.

![A part of iOS related settings](../.gitbook/assets/image%20%2818%29.png)

| Field | Description |
| :--- | :--- |
| **Bundle ID** | Your app bundle ID |
| **App Store Connect shared secret** | A key for receipts' validation and preventing fraud in your app. Read below how to find it |
| **Subscription Key** | A key for using Subscription Offers. Read below how to find it |
| **App Store Connect subscription status URL** | URL that is used to enable [server2server notifications](https://developer.apple.com/documentation/storekit/in-app_purchase/subscriptions_and_offers/enabling_server-to-server_notifications) from the App Store to monitor and respond to users' subscription status changes |
| **Push notifications certificates** | To send Push notifications in [Promo campaigns](../profiles-and-promo-campaigns/promo-campaigns.md) Adapty certificate to sign them. Adapty support both dev and prod certificates |



### App Store Connect shared secret

Adapty uses this key for receipt verification. This key is app-specific, __make sure to generate it for each of your apps.

{% hint style="info" %}
However, you can generate one Primary Shared Secret, and use one key for all your apps. To generate it, go to Users and Access -&gt; [Shared Secret](https://appstoreconnect.apple.com/access/shared-secret) page, and click **Generate** there.
{% endhint %}

Go to **Manage** page in section **In-App Purchases**. On the right, you can see **App-Specific Shared Secret** link, click it, and you'll be able to see or create a new shared secret.

![](../.gitbook/assets/cleanshot-2020-09-14-at-03.56.42-2x.png)

Generate a Shared Secret, copy it, and don't forget to paste it in Adapty Dashboard.

![](../.gitbook/assets/image%20%2813%29.png)



### Subscription Key

The Subscription Key is used for [Promotional offers](https://developer.apple.com/documentation/storekit/in-app_purchase/subscriptions_and_offers/implementing_subscription_offers_in_your_app). For example, you can offer user upfront payment for 6 months with a 40% discount, and after that user will pay the regular subscription price every month. To generate a subscription key:

1. Log in into App Store Connect and open [Users and Access](https://appstoreconnect.apple.com/access/api).

![Click + and generate subscription key](../.gitbook/assets/image%20%2858%29.png)

   2. Generate a Subscription key \(you can name it Adapty\) and download it as a `.p8` file.

   3. Upload `.p8` file to Adapty and copy-paste KEY ID.

![Paste KEY ID and upload .p8 file](../.gitbook/assets/image%20%2829%29.png)

\*\*\*\*

### **App Store Connect subscription status URL**

Apple offers server-to-server notifications, so you can instantly be notified about subscription events.

Adapty helps you with that. The only thing you need to do is to set URL for App Store Server Notifications inside your App Store Connect to Adapty status URL.

1. Copy App Store Connect subscription status URL in Adapty App Settings

![To copy simply click on a copy icon on the right](../.gitbook/assets/image%20%2831%29.png)

{% hint style="info" %}
This URL is specific to each of your apps. So if you have multiple apps, you need to set different URLs
{% endhint %}

     2. Sign-in into your App Store Connect account, choose the app, and go to the **App Information** page in section **General**. Paste subscription status URL into URL for App Store Server Notifications, and save the changes. It may take up to 72 hours for the changes to take effect. 

![](../.gitbook/assets/cleanshot-2020-09-14-at-03.58.27-2x.png)

\*\*\*\*

### **Push notifications**

With Adapty you can automate [promo campaigns](../profiles-and-promo-campaigns/promo-campaigns.md) in Push notifications. For that, Adapty needs a certificate to securely sign notifications. It takes several steps to generate and may take about 15 minutes.

#### Create a signing certificate

Open Keychain Access and on the upper menu choose _Keychain Access -&gt; Certificate Assistant -&gt; Request a Certificate From a Certificate Authority._

![Choose Request a Certificate From a Certificate Authority](../.gitbook/assets/image%20%2895%29.png)

Enter your email and name and save the certificate to a disk. It'll be named like _CertificateSigningRequest.certSigningRequest._ 

{% hint style="success" %}
Create a folder to save all files in one place. For example, name it _Adapty Push Certificates_
{% endhint %}

![Enter email, choose save to disk](../.gitbook/assets/image%20%282%29.png)

#### Create an Identity and Apple Certificate

Open [Apple Developer](https://developer.apple.com) and then [Certificates -&gt; Identifiers](https://developer.apple.com/account/resources/certificates/list).

![Identifiers](../.gitbook/assets/image%20%2893%29.png)

Choose your identifier, activate Push Notifications and hit Save.

![Activating Push Notifications](../.gitbook/assets/image%20%2896%29.png)

{% hint style="warning" %}
Do not configure/edit Push Notifications settings on the page above. It's a legacy stuff. The method below allows you create certificate much easier.
{% endhint %}

Go to Certificates section and start new certificate generation

![Creating a new certificate](../.gitbook/assets/image%20%285%29.png)

Scroll down and select _Apple Push Notification service SSL \(Sandbox & Production\)_

![](../.gitbook/assets/image%20%2894%29.png)

Choose your Identifier and upload a certificated generated on your Mac earlier 

![](../.gitbook/assets/image%20%2882%29.png)

And download a certificate as _aps.cer_ file.

Open the _aps.cer_ file in the Keychain and export in as a p12 file.

![Export certificate as p12 file](../.gitbook/assets/image%20%2892%29.png)

Please be sure that you choose Certificate category! Otherwise you can't export it a p12 file. Yeap, that's super weird.

The last thing, convert your p12 file to a plain text. Open terminal and enter a command

```text
openssl pkcs12 -in cert.p12 -nodes > open_cert.p12
```

change _cert.p12_ to your file name.

And the last, upload a certificate to Adapty.

![Upload p12 certificate](../.gitbook/assets/image%20%2884%29.png)



## 

