---
description: >-
  Learn how to set up push notifications for promo campaigns using Adapty
  Android SDK
---

# Push Notifications

We use Firebase Cloud Messaging \(FCM\) to send push notifications from Adapty. If you need to install it, please refer to the [official documentation](https://firebase.google.com/docs/cloud-messaging/android/client).

{% hint style="warning" %}
Make sure to set [Firebase Cloud Messaging \(FCM\) server key](../../../settings/android-sdk.md#push-notifications) in Adapty Dashboard, without it, we can't send push notifications.
{% endhint %}

To handle push notifications from Adapty, you can inherit from **`AdaptyPushHandler`** like this:

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
class YourAdaptyPushHandler(context: Context) : AdaptyPushHandler(context) {

    override val clickAction = "YOUR_NOTIFICATION_CLICK_ACTION"
    
    override val smallIconResId = R.drawable.ic_notification_small_icon
}
```
{% endtab %}

{% tab title="Java" %}
```java
public class YourAdaptyPushHandler extends AdaptyPushHandler {

    public YourAdaptyPushHandler(@NotNull Context context) {
        super(context);
    }

    @NotNull
    @Override
    public String getClickAction() {
        return "YOUR_NOTIFICATION_CLICK_ACTION";
    }

    @Override
    public int getSmallIconResId() {
        return R.drawable.ic_notification_small_icon;
    }
}
```
{% endtab %}
{% endtabs %}

**`clickAction`** refers to [click\_action](https://firebase.google.com/docs/cloud-messaging/http-server-ref) parameter from Firebase notification message body. You also need to declare the same action in your **`AndroidManifest`** in Activity you want to be launched after the push is clicked:

{% code title="AndroidManifest" %}
```markup
<activity android:name=".YourActivity">
    <!-- your intent-filters-->
    <intent-filter>
        <action android:name="YOUR_NOTIFICATION_CLICK_ACTION" />
        <category android:name="android.intent.category.DEFAULT" />
    </intent-filter>
</activity>
```
{% endcode %}

Optional properties of **`AdaptyPushHandler`** \(or getters in case of Java\) you can override:

* **`largeIcon`** is a nullable Bitmap \(ignored in case of null\), refers to `setLargeIcon` from Notification.Builder
* **`customizedNotificationBuilder`** is a nullable `Notification.Builder` \(ignored in case of null\). In this case, you **don't need** to specify `setSmallIcon`, `setContentIntent`, `setContentTitle` and `setContentText` in your custom builder as it will be overwritten by Adapty SDK. If you override **`customizedNotificationBuilder`** with non-null value, property **`largeIcon`** **is ignored** \(so you need to specify it in your custom builder if needed\).
* **`channelId`** is the ID of the [notification channel](https://developer.android.com/guide/topics/ui/notifiers/notifications.html#ManageChannels) you want promo notifications to be associated with. You can override with the ID of the already existing channel \(if the channel exists it won't be overwritten\). If you pass the ID of an unexisting channel, Adapty will create a new one where ID and name are equal to ID you passed. If you don't override **`channelId`**, Adapty will create its default channel called "Offers".

#### 

### Setup your messaging service to work with promo notifications

You only need to do a few things - register the new Firebase token using **`.refreshPushToken()`** method and delegate handling promo notifications to your **`AdaptyPushHandler`** - just like in the example below:

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
class YourFirebaseMessagingService : FirebaseMessagingService() {

    private val pushHandler: YourAdaptyPushHandler by lazy {
        YourAdaptyPushHandler(this)
    }

    override fun onNewToken(pushToken: String) {
        super.onNewToken(pushToken)
        Adapty.refreshPushToken(pushToken)
    }

    override fun onMessageReceived(message: RemoteMessage) {
        super.onMessageReceived(message)
        if (!pushHandler.handleNotification(message.data)) {
            /*
            here is your logic for other notifications
            that haven't been handled by Adapty
             */
        }
    }
}
```
{% endtab %}
{% endtabs %}



### Handle promo notifications in your Activity

Click on the notification will open the _Activity_ where you specified your _action_. You can handle an Intent to your _Activity_ like this:

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
class YourActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        // your logic
        handleIntent(intent)
    }

    override fun onNewIntent(intent: Intent) {
        super.onNewIntent(intent)
        setIntent(intent)
        handleIntent(intent)
    }
    
    private fun handleIntent(intent: Intent) {
        if (Adapty.handlePromoIntent(intent) { promo, error ->
                // your logic for callback
            }
        ) {
            // your logic for the case user did click on promo notification,
            // for example show loading indicator
        } else {
            // your logic for other cases
        }
    }
}
```
{% endtab %}

{% tab title="Java" %}
```java
public class YourActivity extends AppCompatActivity {

    @Override
    protected void onCreate(@Nullable Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        // your logic
        handleIntent(getIntent());
    }

    @Override
    protected void onNewIntent(Intent intent) {
        super.onNewIntent(intent);
        setIntent(intent);
        handleIntent(intent);
    }

    private void handleIntent(Intent intent) {
        if (Adapty.handlePromoIntent(intent, (promo, error) -> {
            // your logic for callback
            // please note that promo can be null
            return null;
        })) {
            // your logic for the case user did click on promo notification,
            // for example show loading indicator
        } else {
            // your logic for other cases
        }
    }
}
```
{% endtab %}
{% endtabs %}

