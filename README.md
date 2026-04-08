# PayUWebView

PayUWebView is an iOS SDK wrapper around `WKWebView` to open PayU checkout and handle payment callbacks.

## Installation

### Swift Package Manager

Add the package dependency via Xcode:

1. Go to **File → Add Package Dependencies...**
2. Enter the repository URL: `https://github.com/payu-intrepos/PayUWebView-iOS.git`
3. Select version **1.0.0** or later
4. Click **Add Package**

Or add it to your `Package.swift`:

```swift
dependencies: [
    .package(url: "https://github.com/payu-intrepos/PayUWebView-iOS.git", from: "1.0.0")
]
```

## Usage

```swift
import PayUWebView
import WebKit

class PaymentViewController: UIViewController, PayUDelegate {
    
    var webViewManager: WebViewSDK?
    @IBOutlet weak var webView: WKWebView!

    override func viewDidLoad() {
        super.viewDidLoad()
        
        // Initialize the SDK with your WKWebView
        webViewManager = WebViewSDK(webView: webView)
        webViewManager?.delegate = self
        
        // Load payment page
        let postParams = "key=YOUR_KEY&txnid=TXN123&amount=100.00&..."
        webViewManager?.load(urlString: "https://secure.payu.in/_payment", postString: postParams)
    }

    // MARK: - PayUDelegate
    
    func payUonSuccess(_ message: WKScriptMessage) {
        print("Payment Success: \(message.body)")
    }

    func payUonFailure(_ message: WKScriptMessage) {
        print("Payment Failed: \(message.body)")
    }

    func payUonError(_ message: WKScriptMessage) {
        print("Payment Error: \(message.body)")
    }
}
```

## Requirements

- iOS 13.0+
- Swift 5.0+
- Xcode 14.0+

## License

Copyright (c) PayU. All rights reserved.
