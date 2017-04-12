To install the TQG SDK, take the following steps:

0. Make sure you are using CocoaPods v0.39+ and open your Podfile
0. Add `source 'https://github.com/indigotech/Specs.git'` to the top
0. On your project target add `pod "TQGeolocationSDK", "X.X.X"`
0. Locate in your target's build settings on Xcode the option `Embedded Content Contains Swift Code` and set it to `Yes`
0. Run `pod install`

You can see all available versions [here](https://github.com/tq1/br-tqg-ios-public/releases).

Breaking Changes:

1.3.3 - TQGSDK comes with [bitcode](https://developer.apple.com/library/tvos/documentation/IDEs/Conceptual/AppDistributionGuide/AppThinning/AppThinning.html) enabled. Therefore make sure your app target also has this build option enabled so that you don't have any issues while submitting it to Apple's App Store.

2.0.0 - SDK now uses Swift 3
