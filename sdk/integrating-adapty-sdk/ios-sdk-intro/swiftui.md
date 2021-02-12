---
description: Learn how to use Adapty iOS SDK in SwiftUI applications
---

# SwiftUI

### SwiftUI App Lifecycle

Since Xcode 12 and the new SwiftUI, the app can be created without AppDelegate at all.

You can put your configuration code inside **`init`** method.

{% tabs %}
{% tab title="Swift" %}
```swift
import Adapty

@main
struct SwiftUISampleApp: App {
    init() {
        Adapty.activate("PUBLIC_SDK_KEY", customerUserId: "YOUR_USER_ID")
    }

    var body: some Scene {
        WindowGroup {
            ContentView()
        }
    }
}
```
{% endtab %}
{% endtabs %}

Or you can still do it through AppDelegate, but it requires you to create your own **`@UIApplicationDelegateAdaptor`**.

{% tabs %}
{% tab title="Swift" %}
```swift
import Adapty

@main
struct SwiftUISampleApp: App {
    @UIApplicationDelegateAdaptor private var appDelegate: AppDelegate
    
    var body: some Scene {
        WindowGroup {
            ContentView()
        }
    }
}

class AppDelegate: UIResponder, UIApplicationDelegate {
    func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey : Any]? = nil) -> Bool {
        Adapty.activate("PUBLIC_SDK_KEY", customerUserId: "YOUR_USER_ID")
        return true
    }
}
```
{% endtab %}
{% endtabs %}



### Custom dashboard paywalls with SwiftUI

Presenting **`PaywallViewController`** via SwiftUI can be complicated. Here is an example of a very basic implementation.

{% tabs %}
{% tab title="Swift" %}
```swift
import SwiftUI
import Adapty

struct SwiftUISampleView: View {
    @ObservedObject var subscriptionInteractor = SubscriptionInteractor()
    
    var body: some View {
        Text("Sample")
            // bind "isPresented" property and present our controller when needed
            .fullScreenCover(isPresented: $subscriptionInteractor.isPresented) {
                PaywallViewControllerRepresentation(paywallModel: subscriptionInteractor.paywall!, delegate: subscriptionInteractor)
            }
    }
}

class SubscriptionInteractor: ObservableObject {
    var paywall: PaywallModel? = nil
    @Published var isPresented = false
    
    init() {
        Adapty.getPaywalls { (paywalls, products, error) in
            if let paywall = paywalls?.first {
                // receive needed synced paywall
                self.paywall = paywall
                self.isPresented = true
            }
        }
    }
}

extension SubscriptionInteractor: AdaptyPaywallDelegate { ... }

struct PaywallViewControllerRepresentation: UIViewControllerRepresentable {
    let paywallModel: PaywallModel
    let delegate: AdaptyPaywallDelegate
    
    // wrapper over our controller for SwiftUI
    func makeUIViewController(context: Context) -> PaywallViewController {
        return Adapty.getPaywall(for: paywallModel, delegate: delegate)
    }
    
    func updateUIViewController(_ uiViewController: PaywallViewController, context: Context) { }
}
```
{% endtab %}
{% endtabs %}

