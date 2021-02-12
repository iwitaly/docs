---
description: Learn how to set up integration with your webhook
---

# Webhook

Forward [subscription events](./#events) to your own web server.

![](../../.gitbook/assets/image%20%2827%29.png)

When you activate a Webhook, **Adapty** sends a POST verification event in the following format:

```text
{
    adapty_check: {{check_string}}
}
```

Your server must respond with 200 or 201 code and return event containing:

```text
{
    adapty_check_response: {{check_string}}
}
```

with the same `check_string`

After that Adapty sends POST events about your users.



### Event structure

Refer to the [Events section](./#events) to understand which events Adapty sends.

Each event is wrapped into the following structure

```text
{
  "profile_id": "772204ce-ebf6-4ed9-82b0-d8688ab62b01",
  "customer_user_id": "iwitaly@adapty.io",
  "event_type": "non_subscription_purchase",
  "event_datetime": "2020-02-18T18:40:22.000000+0000",
  "event_properties": <event specific properties>
  "event_api_version": 1
}
```

Where

| Property | Type | Description |
| :--- | :--- | :--- |
| **profile\_id** | str | Adapty user ID. |
| **customer\_user\_id** | str | Developer user ID. For example, it can be your user UUID, email, or any other ID. [Learn more](https://github.com/adaptyteam/AdaptySDK-iOS#configure-your-app) about how to pass it using SDK. Null if you didn't set it. |
| **event\_type** | str | Lower cased [event name](./#events). |
| **event\_api\_version** | int | Current Adapty API version. The current value is _1._ |
| **event\_properties** | json | JSON of [event properties](./#properties). |



### Event names mapping

You can change the mapping from default Adapty [event](./#events) names to your own

![Changing event name](../../.gitbook/assets/image%20%2838%29.png)

name can be any string except a blank.

