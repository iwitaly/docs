---
description: >-
  In this topic we describe how you can handle most of the SKError's errors
  e.g.: SKErrorPaymentCancelled, SKErrorInvalidOfferIdentifier, SKErrorUnknown,
  etc.
---

# Error handling \(SKError, NSError, Error\)

Adapty SDK has it's own wrapper for all kind of errors, called **`AdaptyError`**. Basically, every error returned by an SDK is **`AdaptyError`**. It has two useful properties: **`originalError`** and **`adaptyErrorCode`**, described below.

### originalError

It contains original error in case you need the original one to work with. Can be [SKError](https://developer.apple.com/documentation/storekit/skerror), [NSError](https://developer.apple.com/documentation/foundation/nserror) or just general Swift [Error](https://developer.apple.com/documentation/swift/error). This property is optional, since some errors can be generated directly by SDK, like inconsistent or missing data and won't have original error around which wrapper was initially built.

### adaptyErrorCode 

This one can be used to handle common issues, like:

* invalid credentials
* network errors
* cancelled payments
* billing issues
* invalid receipt
* and much more

It's pretty easy to check error for specific code and react to them accordingly.

```swift
import Adapty

Adapty.makePurchase(product: product) { (purchaserInfo, receipt, appleValidationResult, _, error) in
    if error?.adaptyErrorCode == .paymentCancelled {
        // purchase was cancelled
        // you can offer discount to your user or remind them later
    }
}
```

## Most common errors and how to handle them

### StoreKit errors

#### AdaptyErrorеCode.paymentCancelled

Corresponds to [**`SKError.Code.paymentCancelled`**](https://developer.apple.com/documentation/storekit/skerror/code/paymentcancelled).

**Issue:**  
User cancelled their purchase and was not charged.

**Workaround:**  
No action required, but in terms of the business logic you can offer discount to your user or remind them later.

#### AdaptyErrorCode.cantReadReceipt

**Issue:**  
There is no valid receipt available on the device. Can be an issue during sandbox testing.

**Workaround:**  
In sandbox, you won't have a valid receipt file until you actually make a purchase, so make sure you did one before accessing it. During sandbox testing also make sure you signed in on device with a valid Apple sandbox account.

#### AdaptyErrorCode.invalidOfferIdentifier

Corresponds to [**`SKError.Code.invalidOfferIdentifier`**](https://developer.apple.com/documentation/storekit/skerror/code/invalidofferidentifier).

**Issue:**  
The offer [`identifier`](https://developer.apple.com/documentation/storekit/skpaymentdiscount/3043528-identifier) is not valid. For example, you have not set up an offer with that identifier in the App Store, or you have revoked the offer.

**Workaround:**  
Make sure you set up desired offers in AppStore connect and pass a valid offer identifier.

#### AdaptyErrorCode.noProductsFound

**Issue:**  
We were unable to fetch any products from StoreKit.

**Workaround:**  
Make sure:  
– you created products in AppStore connect;  
– you added products in Adapty dashboard;  
–  you running simulator under iOS 14 or if you want to continue using iOS 14 make sure you run it on a real device.

#### AdaptyErrorCode.missingOfferSigningParams

**Issue:**  
Signature, generated for purchase with promotional offer was missing or invalid.

**Workaround:**  
Make sure you've uploaded [Subscription Key](https://docs.adapty.io/settings/ios-sdk#subscription-key) in Adapty Dashboard for using promotional offers.

## General error list

### StoreKit errors

| Error | Code | Description |
| :--- | :--- | :--- |
| unknown | 0 | Error code indicating that an unknown or unexpected error occurred. |
| clientInvalid | 1 | Error code indicating that the client is not allowed to perform the attempted action. |
| paymentCancelled | 2 | Error code indicating that the user canceled a payment request. |
| paymentInvalid | 3 | Error code indicating that one of the payment parameters was not recognized by the App Store. |
| paymentNotAllowed | 4 | Error code indicating that the user is not allowed to authorize payments. |
| storeProductNotAvailable | 5 | Error code indicating that the requested product is not available in the store. |
| cloudServicePermissionDenied | 6 | Error code indicating that the user has not allowed access to Cloud service information. |
| cloudServiceNetworkConnectionFailed | 7 | Error code indicating that the device could not connect to the network. |
| cloudServiceRevoked | 8 | Error code indicating that the user has revoked permission to use this cloud service. |
| privacyAcknowledgementRequired | 9 | Error code indicating that the user has not yet acknowledged Apple’s privacy policy for Apple Music. |
| unauthorizedRequestData | 10 | Error code indicating that the app is attempting to use a property for which it does not have the required entitlement. |
| invalidOfferIdentifier | 11 | Error code indicating that the offer identifier is invalid. |
| invalidSignature | 12 | Error code indicating that the signature in a payment discount is not valid. |
| missingOfferParams | 13 | Error code indicating that parameters are missing in a payment discount. |
| invalidOfferPrice | 14 | Error code indicating that the price you specified in App Store Connect is no longer valid. |
| noProductIDsFound | 1000 | No In-App Purchase product identifiers were found. |
| noProductsFound | 1001 | No In-App Purchases were found. |
| productRequestFailed | 1002 | Unable to fetch available In-App Purchase products at the moment. |
| cantMakePayments | 1003 | In-App Purchases are not allowed on this device. |
| noPurchasesToRestore | 1004 | No purchases to restore. |
| cantReadReceipt | 1005 | Can't find a valid receipt. |
| productPurchaseFailed | 1006 | Product purchase failed. |
| missingOfferSigningParams | 1007 | Missing offer signing required params. |
| fallbackPaywallsNotRequired | 1008 | Fallback paywalls are not required. |

### Network errors

| Error | Code | Description |
| :--- | :--- | :--- |
| emptyResponse | 2000 | Response is empty. |
| emptyData | 2001 | Request data is empty. |
| authenticationError | 2002 | You need to be authenticated to perform requests. |
| badRequest | 2003 | Bad request. |
| outdated | 2004 | The url you requested is outdated. |
| failed | 2005 | Network request failed. |
| unableToDecode | 2006 | We could not decode the response. |
| missingParam | 2007 | Missing some of the required params. |
| invalidProperty | 2008 | Received invalid property data. |
| encodingFailed | 2009 | Parameters encoding failed. |
| missingURL | 2010 | Request url is nil. |

### General errors

| Error | Code | Description |
| :--- | :--- | :--- |
| analyticsDisabled | 3000 | We can't handle analytics events, since you've opted it out. |

