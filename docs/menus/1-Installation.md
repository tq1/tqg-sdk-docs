To install the TQG SDK, take the following steps:

- Make sure you are using CocoaPods v0.39.0 and open your Podfile
- Add `source 'https://github.com/indigotech/Specs.git'` to the top
- Before adding the TQGeolocationSDK, please make sure your Podfile is working. Erase your project DerivedData folder, clean the project and run pod install. If the project can build and run, go to the next step
- Add the following to your Podfile (sources: https://github.com/CocoaPods/CocoaPods/issues/3646, https://github.com/CocoaPods/CocoaPods/issues/4331):

```ruby
target 'Your_Target_Name' do
  use_frameworks!

  pod 'TQGeolocationSDK', '1.3.0'

  post_install do |installer|
    installer.pods_project.targets.each do |target|
      target.build_configurations.each do |config|
        config.build_settings.delete 'CODE_SIGN_IDENTITY[sdk=iphoneos*]'
        config.build_settings['EXPANDED_CODE_SIGN_IDENTITY'] = ""
        config.build_settings['CODE_SIGNING_REQUIRED'] = "NO"
        config.build_settings['CODE_SIGNING_ALLOWED'] = "NO"
      end
    end
  end
end
```
- Run pod install

Possible build errors:

0. If you receive an error such as: 'TQTStylesheets.h' file not found. 
You must, after adding use_frameworks!, change all your imports that refer to Pods to the following format, to read from the framework instead of static library: `<Pod_Name/Header_filename.h>`
For instance:
Change: `#import “TQTStylesheets.h”`
To: `#import <TQTStylesheets/TQTStylesheets.h>`
NOTE: It doesn't apply for the TQ1SDK Pod, since this Pod uses a static library. So just use, for example: `#import <TQ1Inbox.h>`

0. After changing the imports to the format specified above, you receive the error: `'TQTStylesheets/TQTStylesheets.h' file not found`. 
This error also happens if you use "link_with" in your Podfile. Since "link_with" was introduced only in Pods 0.39, and will be discontinued in Pods 1.0.0 (replaced by abstract_target), the solution is to just organize your Podfile without using "link_with".

0. Everything compiles, but when you run the project it crashes with the error:
`dyld: Library not loaded: @rpath/libswiftContacts.dylib
  Referenced from: /Users/raphaelpetegrosso/Library/Developer/CoreSimulator/Devices/11321430-86AF-41AD-8231-E13E5245497D/data/Containers/Bundle/Application/BD8B1C09-8DEC-4A22-B64D-BABEC45C9547/TQGTest.app/Frameworks/libswiftUIKit.dylib
  Reason: image not found`
To solve this, open your build settings and search for the entry "Embedded Content Contains Swift Code". Set it to YES. By setting this option, you add some dylib needed by Swift to your build, such as "libswiftUIKit.dylib", shown in the error message.
More information here: https://developer.apple.com/library/ios/qa/qa1881/_index.html
NOTE: This problem was reported when using cocoapods 0.39.0.beta.4, but didn't happen for 0.39.0.

You can import the framework by using the following line: `#import <TQGeolocationSDK/TQGeolocationSDK-Swift.h>`
