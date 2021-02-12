---
description: >-
  Learn how to import Adapty React Native SDK in your app, configure it, and set
  up logging
---

# Configuration

To initialize Adapty SDK, import **`activateAdapty`** function and call it in **a core component**, such as **`App.tsx`**. Wrap this function with **`useEffect(callback,[])`**  to make sure Adapty initializes only once.

{% tabs %}
{% tab title="TypeScript" %}
{% code title="/src/App.tsx" %}
```typescript
import { activateAdapty } from 'react-native-adapty';

const App: React.FC = () => {
  ...
  useEffect(() => {
    activateAdapty({ sdkKey: 'PUBLIC_SDK_KEY' });
  },[]);
  ...
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

**`activateAdapty`** has several more parameters:

* **`sdkKey` — Public SDK key**. Required. Can be found in your app settings in [Adapty Dashboard](https://app.adapty.io/settings/general) `App settings` &gt; `General`
* **`customerUserId`** — **Customer user ID.** Optional. An identifier of the user in your system. We send it in subscription and analytical [events](), to attribute events to the right profile. You can also find customers by **`customerUserId`** in the [Profiles](../../../profiles-and-promo-campaigns/profiles.md) section
* **`observerMode`** — **Observer mode.** Optional. Default is **`false`**. Controls [Observer mode](../ios-sdk-intro/ios-sdk-observer-mode.md). Turn it on if you handle purchases and subscription status yourself and use Adapty for sending subscription events and analytics
* **`logLevel`** — **Debugging log level**. Optional. Default is **`'none'`**. Adapty logs errors and other important information to help you understand what is going on. Possible values are **`'verbose'`**, **`'errors'`** or **`'none'`**. If on, errors are displayed within platform-specific IDE \(Xcode or Android Studio\)

{% tabs %}
{% tab title="TypeScript" %}
```typescript
activateAdapty({
  sdkKey: 'PUBLIC_SDK_KEY', // string
  customerUserId: 'YOUR_USER_ID', // string | undefined
  observerMode: true, // boolean
  logLevel: "verbose", // 'verbose' | 'errors' | 'none'
});
```
{% endtab %}
{% endtabs %}



