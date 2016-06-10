To install the TQG SDK, take the following steps:

0. Make sure you are using CocoaPods v0.39+ and open your Podfile
0. Add `source 'https://github.com/indigotech/Specs.git'` to the top
0. On your project target add `pod "TQGeolocationSDK", "X.X.X"`
0. Locate in your target's build settings on Xcode the option `Embedded Content Contains Swift Code` and set it to `Yes`
0. Run `pod install`

You can see all available versions [here](https://github.com/tq1/br-tqg-ios-public/releases).