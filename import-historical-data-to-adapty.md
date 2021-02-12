# Import Historical Data to Adapty

After you install [Adapty SDK](https://github.com/adaptyteam/AdaptySDK-iOS) and release the app, you can find your users and subscribers in [Profiles](profiles-and-promo-campaigns/profiles.md). But what if you have legacy infrastructure and want to migrate to Adapty? Or just want to see your existing data in Adapty?

You can export your data to a CSV file and then import it to Adapty. Let's see how to do that.

### Data format

Export data to a CSV file with a format in [this](https://docs.google.com/spreadsheets/d/162LMI9D7-BP63Jkllj2AtpaD7FQFa0-V-Yht1U65Ojs/edit?usp=sharing) file \(Google doc file\). Fields without description are self-explained \(we hope they are\). 

| Field name | Description |
| :--- | :--- |
| **user\_id** | Id of your user |
| **subscription\_expiration\_date** | The date of subscription expiration, i.g. next charging date, datetime with timezone \(2020-12-31T23:59:59-06:00\) |
| **created\_at** | Datetime of profile creation \(2019-12-31T23:59:59-06:00\) |
| **birthday** | date \(2000-12-31\) |
| **email** |  |
| **facebook\_user\_id** |  |
| **gender** | f\|m |
| **phone\_number** |  |
| **first\_name** |  |
| **last\_name** |  |
| **last\_seen** | datetime with timezone \(2020-12-31T23:59:59-06:00\) |
| **idfa** | iOS Identifier for advertiser |
| **idfv** |  |
| **advertising\_id** | It's similar to idfa, but for Android |
| **amplitude\_user\_id** |  |
| **amplitude\_device\_id** |  |
| **mixpanel\_user\_id** |  |
| **appmetrica\_profile\_id** |  |
| **appmetrica\_device\_id** |  |
| **attribution\_source** | appsflyer\|adjust\|branch\|apple\_search\_ads |
| **attribution\_status** | organic\|non\_organic\|unknown |
| **attribution\_channel** | \*\*\*\* |
| **attribution\_campaign** | \*\*\*\* |
| **attribution\_ad\_group** | \*\*\*\* |
| **attribution\_ad\_set** | \*\*\*\* |
| **attribution\_creative** |  |
| **apple\_receipt\_encoded** |  |
| **google\_product\_id** |  |
| **google\_purchase\_token** |  |
| **google\_is\_subscription** | 1\|0 |

The only required field is **user\_id**. However, to see all transaction history you need to specify **apple\_receipt\_encoded** or **google\_product\_id+google\_purchase\_token+google\_is\_subscription,** without them Adapty won't be able to fetch transactions.

### Import data to Adapty

Right now we don't have an automatic tool for that. Please contact us using the website \(we use Intercom in the bottom right corner\) or just email us at contact@adapty.io.

