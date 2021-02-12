---
description: >-
  Learn how to fetch and display products from paywalls in your app using Adapty
  React Native SDK. With Adapty you can dynamically change the products visible
  to your users without new app releases
---

# Displaying Products

Adapty allows you to remotely configure the products that will be displayed in your app. This way you don't have to hard code the products and can dynamically change offers or run A/B tests without app releases.

{% hint style="warning" %}
Make sure you've added the [products](https://docs.adapty.io/purchase-infrastructure/product) and [paywalls](https://docs.adapty.io/purchase-infrastructure/paywall) in Adapty Dashboard before fetching the products.
{% endhint %}

To fetch products call **`adapty.paywalls.getPaywalls()`** method:

{% tabs %}
{% tab title="TypeScript" %}
```typescript
try {
  const { paywalls, products } = await adapty.paywalls.getPaywalls(
    { forceUpdate: false }
  );
} catch (error: AdaptyError) {}
```
{% endtab %}
{% endtabs %}

Request parameters:

* **`{forceUpdate}`**  — **Force update**. Optional. If you want to force fetching from the server. Data from a local cache would be used otherwise.

Response parameters:

* **`paywalls`** — array of **`AdaptyPaywall`**. Each object contains the list of the products, paywall's identifier, custom payload, and several other properties. All you need to display the products in your app is to get a paywall by its identifier, retrieve the products, and display them
* **`products`** — array of **`AdaptyProduct`**. Each object contains a product identifier, price, currency, title, and many other product options. Generally, you don't have to use this response parameter as all the products should be stored in the paywalls.

{% hint style="info" %}
Every time the data is fetched from a remote server, it will be stored in the local cache. This way, you can display the products even when the user is offline.
{% endhint %}

{% hint style="warning" %}
Since the paywalls are configured remotely, the available products, the number of the products, and the special offers \(eg free trials\) can change over time. Make sure your code handles these scenarios. For example, if you get 2 products, the 2 products will be displayed, but when you get 3, all of them should be displayed without code changes.

**Don't hard code product ids**, you won't need them.
{% endhint %}



### Example component

{% tabs %}
{% tab title="TypeScript" %}
```typescript
import React, { useState, useEffect } from 'react';
import { View, Text } from 'react-native';
import { adapty, AdaptyPaywall } from 'react-native-adapty';

const Component: React.FC = () => {
  const [paywall, setPaywall] = useState<AdaptyPaywall | undefined>();
    
  useEffect(() => {
    async function fetchPaywall() {
      const { paywalls } = await adapty.paywalls.getPaywalls();
      const bestPaywall = paywalls.find(paywall => 
        paywall.developerId === 'myFavoritePaywall'
      );
    
      setPaywall(bestPaywall);
    }
    fetchPaywall();
    },[]);
    
    function renderProducts() {
      if (!paywall) {
        return null;
      }
        
      return paywall.products.map((product) =>
        <Text>{product.localizedTitle}</Text>
      );
    }

    return <View>{renderProducts()}</View>;
}

```
{% endtab %}
{% endtabs %}



### Paywall analytics

{% hint style="warning" %}
By default, Adapty SDK sends**`paywallShow`** event which is accumulated in visitors metrics after every **`.getPaywalls()`** call. It works automatically, but it's incorrect because the user not necessarily was shown the paywall.

We strongly recommend disable automatic tracking and send these events manually for precise metric calculations.
{% endhint %}

First, disable automatic tracking by setting the flag **`AdaptyAutomaticPaywallsScreenReportingEnabled`** to **`false`** in **`Info.plist`** \(iOS\) and  **`AndroidManifest.xml`** \(Android\):

{% tabs %}
{% tab title="Info.plist" %}
```markup
<dict>
  ...
    
  <key>AdaptyAutomaticPaywallsScreenReportingEnabled</key>    
  <false/>
  
</dict>
```
{% endtab %}

{% tab title="AndroidManifest.xml" %}
```markup
<application ...>
       ...
       <meta-data
              android:name="AdaptyAutomaticPaywallsScreenReportingEnabled"
              android:value="false" />
</application>
```
{% endtab %}
{% endtabs %}

Next, whenever you show a paywall to your user, call **`adapty.paywalls.logShow(paywall.variationId)`** to log **`paywallShow`** event related to your paywall.

{% tabs %}
{% tab title="TypeScript" %}
```typescript
const Paywall: React.FC = () => {
  ...
  useEffect(() => {
    async function fetchPaywall() {
      const { paywalls } = await adapty.paywalls.getPaywalls();
      const bestPaywall = paywalls.find(paywall => 
        paywall.developerId === 'myFavoritePaywall'
      );
            
      setPaywall(bestPaywall);
            
      adapty.paywalls.logShow(bestPaywall.variationId);
    }
    fetchPaywall();
  },[]);
  ...
}
```
{% endtab %}
{% endtabs %}

