# KindeSDK

[![Version](https://img.shields.io/cocoapods/v/KindeSDK.svg?style=flat)](https://cocoapods.org/pods/KindeSDK)
[![License](https://img.shields.io/cocoapods/l/KindeSDK.svg?style=flat)](https://cocoapods.org/pods/KindeSDK)
[![Platform](https://img.shields.io/cocoapods/p/KindeSDK.svg?style=flat)](https://cocoapods.org/pods/KindeSDK)

Integrate Kinde authentication with your iOS app. Simply **configure**, **register**, **login**, and **logout**, and authentication state is securely stored on the iOS keychain across app restarts.

## Requirements

- iOS 13+
- Xcode 12+
- Swift 5+

## Installation

### Cocoapods

KindeSDK is available through [CocoaPods](https://cocoapods.org). To install
it, simply add the following line to your Podfile:

```ruby
pod 'KindeSDK'
```

Please note that `KindeSDK` is typically used with Cocoapods dynamic linking (`use_frameworks!`), as it takes a dependency on `AppAuth`.
If integrating with other pods that require static linking, follow the instructions provided by Cocoapods.

### Swift Package Manager

With [Swift Package Manager](https://swift.org/package-manager), 
add the following `dependency` to your `Package.swift`:

```swift
dependencies: [
    .package(url: "https://github.com/kinde-oss/kinde-sdk-ios.git", from: "1.1")
]
```

## Configuration

The Kinde `Auth` service is configured with an instance of the `Config` class. The example project uses the bundled `kinde-auth.json` for configuration.
Alternatively, configuration can be supplied in JSON format with the bundled `KindeAuth.plist`.
Enter the values from the [App Keys](https://kinde.com/docs/the-basics/getting-app-keys) page for your Kinde business: E.g.,

```
{
  "issuer": "https://{your-business}.kinde.com",
  "clientId": "{your-client-id}",
  "redirectUri": "{your-url-scheme}://kinde_callback",
  "postLogoutRedirectUri": "{your-url-scheme}://kinde_logoutcallback",
  "scope": "openid profile email offline",
  "audience": "{your-audience}"
}
```

Note: `your_url_scheme` can be any valid custom URL scheme, such as your app's bundle ID or an abbreviation.
It must match the scheme component of the _Allowed callback URLs_ and _Allowed logout redirect URLs_
you configure in your [App Keys](https://kinde.com/docs/the-basics/getting-app-keys) page for your Kinde business: E.g.,

```
{
  "issuer": "https://app.example.com",
  "clientId": "abc@live",
  "redirectUri": "com.example.App://kinde_callback",
  "postLogoutRedirectUri": "com.example.App://kinde_logoutcallback",
  "scope": "openid profile email offline"
  "audience": "https://app.example.com"
}
```
Before `Auth` or any Kinde Management APIs can be used, a call to `Auth.configure()` must be made, typically in `AppDelegate`
as part of `application(launchOptions)` for a UIKit app, or the `@main` initialization logic for a SwiftUI app.
Note: `audience` can be optional

## Kinde Management API

KindeSDK includes a client for the [Kinde Management API](./KindeSDK/Classes/KindeManagementAPI/README.md).
This client is generated by the [OpenApi Genenerator](https://openapi-generator.tech/docs/generators/swift5/).

Support for bearer token authentication is implemented by classes with the naming convention `Bearer`\*, according to the OpenAPI Generator [recommendation](https://github.com/OpenAPITools/openapi-generator/wiki/FAQ#how-do-i-implement-bearer-token-authentication-with-urlsession-on-the-swift-api-client).

Functions/methods targeting the Management API can only be accessed with tokens generated by the Client Credentials Auth flow at the moment. Since this SDK does not support the Client Credential flow, Management API functions are not available for use. In the future, tokens obtained via other flows would also be able to access the management API functions/methods.

## Development

Observe [Swift conventions](https://www.swift.org/documentation/api-design-guidelines/) where possible.

## Author

Kinde, kinde.com

## License

KindeSDK is available under the MIT license. See the LICENSE file for more info.
