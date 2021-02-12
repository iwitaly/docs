---
description: >-
  Configure App Store Connect integration to use Basic Analytics. Import
  products of your app
---

# App Store Connect

Give Adapty access to App Store Connect, and instantly get access to Analytics.

Apple does not provide oAuth API for App Store Connect. That is why several steps are required to set up manually. Fortunately, you do them only once and it takes under 5 minutes.

![Example of filled ](../.gitbook/assets/image%20%2863%29.png)

{% hint style="success" %}
#### Is my data safe?

Please read [how we store data and process it](../faq.md#is-my-data-safe). Your privacy matters to us.
{% endhint %}

### 

### Issuer ID, API key, ID Private key

All these variables are accessible on a single page.

1. Open your [App Store Connect](https://appstoreconnect.apple.com/), and log in with your account.
2. Choose the application, and then go to [Users and Access](https://appstoreconnect.apple.com/access/api).

![Click on the upper left menu and choose Users and Access](../.gitbook/assets/image%20%2839%29.png)

And then hit Keys

![](../.gitbook/assets/image%20%2841%29.png)

3. Now you need to generate API Key for us to have access to your data on your behalf

{% hint style="warning" %}
Be sure you are an admin of the App Store Connect account. Otherwise you won't be able to generate a key.
{% endhint %}

![](../.gitbook/assets/image%20%2886%29.png)

{% hint style="danger" %}
Don't forget to set Sales and Reports access scope while generating a key.
{% endhint %}

4. That's it! Now you can download a key as a `.p8` file. **DO NOT DELETE THIS KEY**, ****save it in a secure place. You'll be able to download it only once. [Learn more](https://developer.apple.com/documentation/appstoreconnectapi/creating_api_keys_for_app_store_connect_api) about this key.

You should now have a page similar to this one

![Users and Access Keys after key generation](../.gitbook/assets/image%20%2847%29.png)

From this page, you should get

* **Issuer ID** — basically it's ID of a user who issued the key
* **Key ID** — Apple's internal identifies of the key
* **Private key** — _that you've downloaded_

### 

### Vendor number

Now you need a vendor number. Just go to [Payment and financial reports](https://appstoreconnect.apple.com/itc/payments_and_financial_reports#/) and you'll see it on the upper left corner.

![Vendor number is blurred](../.gitbook/assets/image%20%2891%29.png)

