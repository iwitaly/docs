# Events

After installing [Adapty SDK](../../sdk/integrating-adapty-sdk/) and connecting [Subscription Status URL](../../settings/ios-sdk.md#app-store-connect-subscription-status-url) for iOS and [Real-time developer notifications \(RTDN\)](../../settings/android-sdk.md#real-time-developer-notifications-rtdn) for Android, Adapty receives info about your customer behavior and converts it into 16 human-readable events.

| Event Name | Description |
| :--- | :--- |
| **subscription\_initial\_purchase** | User has activated a subscription without a trial period i.e. he was billed instantly |
| **subscription\_renewed** | Subscription was renewed and user was charged. For both trial and non-trial subscriptions this event is sent starting from the second billing |
| **subscription\_cancelled** | User has cancelled a subscription |
| **trial\_started** | User has activated a trial subscription |
| **trial\_converted** | Trial period has ended and user was billed i.e. first purchase was made |
| **trial\_cancelled** | User cancelled subscription during trial period |
| **non\_subscription\_purchase** | Any non-subscription purchase e.g. lifetime access or consumable product such as coins |
| **billing\_issue\_detected** | User was tried to charge, but billing issue happened. Usually it means user doesn't have enough card balance |
| **entered\_grace\_period** | Payment was not successful and user entered into a grace period. User still has access to premium function of your app until grace period finished |
| **auto\_renew\_off** | User turned off subscription auto renew during trial. User still has access to premium function of your app until TRIAL\_CANCELLED |
| **auto\_renew\_on** | User turned on subscription auto renew during trial period |
| **auto\_renew\_off\_subscription** | User turned off subscription auto renew. User still has access to premium function of your app until SUBSCRIPTION\_CANCELLED |
| **auto\_renew\_on\_subscription** | User turned on subscription auto renew |
| **subscription\_refunded** | Subscription was refunded \(e.g. by Apple support\) |
| **non\_subscription\_purchase\_refunded** | Non-subscription purchase was refunded |
| **subscription\_paused** | User activated [subscription pause](https://developer.android.com/google/play/billing/subs#pause) \(Android only\) |

{% hint style="info" %}
**SUBSCRIPTION\_CANCELLED** event means that the subscription completely finished and the user has no longer access to the premium features of the app. When user unsubscribes, **AUTO\_RENEW\_OFF** or **AUTO\_RENEW\_OFF\_SUBSCRIPTION** is sent. The same logic applied to **TRIAL\_CANCELLED.**
{% endhint %}

The events above fully cover the users' state in terms of purchases. Let's look at some examples.

#### Example 1

_The user activated a monthly subscription on April 1st with 7 days trial. On the 4th day, he unsubscribed._

In that case following events will be sent:

1. trial\_started on April 1st
2. auto\_renew\_off on 4th April
3. trial\_cancelled on 7th April

#### Example 2

_The user activated a monthly subscription on April 1st with 7 days trial. On the 10th day, he unsubscribed._

In that case following events will be sent:

1. trial\_started on April 1st
2. trial\_converted on April 7th
3. auto\_renew\_off\_subscription on April 10th
4. subscription\_cancelled on May 1st

### Properties

<table>
  <thead>
    <tr>
      <th style="text-align:left">Property</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>price_usd</b>
      </td>
      <td style="text-align:left">float</td>
      <td style="text-align:left">Product price before Apple/Google cut. Revenue.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>proceeds_usd</b>
      </td>
      <td style="text-align:left">float</td>
      <td style="text-align:left">Product price after Apple/Google cut. Net revenue.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>transaction_id</b>
      </td>
      <td style="text-align:left">str</td>
      <td style="text-align:left">A unique identifier for a transaction such as a purchase or renewal.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>original_transaction_id</b>
      </td>
      <td style="text-align:left">str</td>
      <td style="text-align:left">The transaction identifier of the original purchase.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>purchase_date</b>
      </td>
      <td style="text-align:left">ISO 8601 date</td>
      <td style="text-align:left">The date and time of product purchase.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>original_purchase_date</b>
      </td>
      <td style="text-align:left">ISO 8601 date</td>
      <td style="text-align:left">The date and time of the original purchase.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>environment</b>
      </td>
      <td style="text-align:left">str</td>
      <td style="text-align:left">Could be <em>Sandbox</em> or <em>Production.</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>vendor_product_id</b>
      </td>
      <td style="text-align:left">str</td>
      <td style="text-align:left">Product id in Apple/Google store.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>event_datetime</b>
      </td>
      <td style="text-align:left">ISO 8601 date</td>
      <td style="text-align:left">The date and time of event.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>store</b>
      </td>
      <td style="text-align:left">str</td>
      <td style="text-align:left">Could be <em>app_store</em> or <em>play_store.</em>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>trial_duration</b>
      </td>
      <td style="text-align:left">str</td>
      <td style="text-align:left">Duration of a trial period in days. Sent in a format <em>&quot;{} days&quot; </em>,
        for example, &quot;7 days&quot;.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>cancellation_reason</b>
      </td>
      <td style="text-align:left">str</td>
      <td style="text-align:left">
        <p>A reason why the user canceled a subscription.</p>
        <p>Can be
          <br />iOS &amp; Android
          <br /><em>voluntarily_cancelled</em>, <em>billing_error</em>, <em>refund</em>
          <br
          /><a href="https://developer.apple.com/library/archive/releasenotes/General/ValidateAppStoreReceipt/Chapters/ReceiptFields.html">iOS</a>
          <br
          /><em>price_increase</em>, <em>product_was_not_available</em>, <em>unknown<br /></em>Android
          <br
          /><em>new_subscription_replace</em>, <em>cancelled_by_developer</em>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>subscription_expires_at</b>
      </td>
      <td style="text-align:left">ISO 8601 date</td>
      <td style="text-align:left">The Expiration date of subscription. Usually in the future.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>consecutive_payments</b>
      </td>
      <td style="text-align:left">int</td>
      <td style="text-align:left">The number of periods, that a user is subscribed without interruptions.
        Includes the current period.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>rate_after_first_year</b>
      </td>
      <td style="text-align:left">bool</td>
      <td style="text-align:left">Boolean indicates that a vendor reduces cuts to 15%. Apple and Google
        have 30% first-year cut and 15% after it.</td>
    </tr>
  </tbody>
</table>

Each event ****has the following properties:

`transaction_id, original_transaction_id, purchase_date, original_purchase_date, environment, vendor_product_id, event_datetime, store`

In addition. some events have additional properties.

| Event Name | Properties |
| :--- | :--- |
| **subscription\_initial\_purchase** | price\_usd, proceeds\_usd, subscription\_expires\_at, consecutive\_payments, rate\_after\_first\_year, trial\_duration |
| **subscription\_renewed** | price\_usd, proceeds\_usd, subscription\_expires\_at, consecutive\_payments, rate\_after\_first\_year, trial\_duration |
| **subscription\_cancelled** | cancellation\_reason, trial\_duration |
| **trial\_started** | subscription\_expires\_at, trial\_duration |
| **trial\_converted** | price\_usd, proceeds\_usd, subscription\_expires\_at, consecutive\_payments, rate\_after\_first\_year, trial\_duration |
| **trial\_cancelled** | cancellation\_reason, trial\_duration |
| **non\_subscription\_purchase** | price\_usd, proceeds\_usd |
| **billing\_issue\_detected** | subscription\_expires\_at, trial\_duration |
| **entered\_grace\_period** | subscription\_expires\_at, trial\_duration |

Event example

```text
{
    "price_usd": 9.99,
    "proceeds_usd": 6.99,
    "transaction_id": "1000000628581600",
    "original_transaction_id": "1000000628581600",
    "purchase_date": "2020-02-18T18:40:22.000000+0000",
    "original_purchase_date": "2020-02-18T18:40:22.000000+0000",
    "environment": "Sandbox",
    "vendor_product_id": "premium",
    "event_datetime": "2020-02-18T18:40:22.000000+0000",
    "store": "app_store"
}
```

Adapty send events to your [server](webhook.md) and [3rd party analytical systems](3rd-party-analytics.md).

{% page-ref page="webhook.md" %}

{% page-ref page="3rd-party-analytics.md" %}

