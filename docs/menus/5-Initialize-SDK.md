## Configure

To start TQG SDK you must set the desired configuration preference:

 - APP_ID: The application identifier string.
 - TRIGGER_MODE (Optional): Can choose from 3 types of trigger mode - BOTH, LOCAL_ONLY, REMOTE_ONLY
 - ENVIRONMENT: The environment which the app will run -  PRODUCTION, STAGING, QA, DEVELOPMENT

This configuration are set by calling the following methods:

Swift:
```
TQGeoTracker.sharedInstance.configure(<APP_ID>, triggerMode: TriggerModes.<TRIGGER_MODE>, environment: TQEnvironments.<ENVIRONMENT>)
```

Objective-C:
```
[[TQGeoTracker sharedInstance] configure:<APP_ID> triggerMode: TriggerModes.<TRIGGER_MODE> environment: TQEnvironments.<ENVIRONMENT>];
```

This configuration method are called in `didFinishLaunchingWithOptions` method.

## Set Parameters

Also you can set some parameters option (Not required):

  - ACCURACY: (CLLocationAccuracy) The accuracy used to track the user's location on foreground. (Default: kCLLocationAccuracyHundredMeters)
  - DISTANCE_FILTER: (CLLocationDistance) The minimum distance in meters that the user must move to trigger a location update. (Default: 50)
  - CACHE_EXPIRATION: (Int) The time interval in seconds before the cache expires. (Default: 3600)
  - ZONE_INTERVAL: (NSNumber) The lat/lng interval of zones used by the server. (Default: 0.2)
  - LINGER_TIME: (Int) The interval in seconds in which linger events are triggered. (Default: 300)
  - MAX_LINGER_TIME: (Int) The maximum interval in seconds that the linger can have before disabling. (Default: 7200)
  - REQUEST_RETRY_INTERVAL: (NSTimeInterval) The interval in seconds before retrying to perform a request. (Default: 120)

This parameters can be set by calling the following methods:

Swift:
```
TQGeoTracker.sharedInstance.setParameters(<ACCURACY>, distanceFilter: <DISTANCE_FILTER>, cacheExpiration: <CACHE_EXPIRATION>, zoneInterval: <ZONE_INTERVAL>, lingerTime: <LINGER_TIME>, maxLingerTime: <MAX_LINGER_TIME>, requestRetryInterval: <REQUEST_RETRY_INTERVAL>)
```

Objective-C:
```
[[TQGeoTracker sharedInstance] setParameters:<ACCURACY> distanceFilter: <DISTANCE_FILTER> cacheExpiration: <CACHE_EXPIRATION> zoneInterval: <ZONE_INTERVAL> lingerTime: <LINGER_TIME> maxLingerTime: <MAX_LINGER_TIME> requestRetryInterval: <REQUEST_RETRY_INTERVAL>];
```

**ATTENTION: These settings should match the server configuration and may break functionality if incorrect, change with caution.**

## Start
After configure, just call the method `start` to initiate the location tracker.

Swift:
```
TQGeoTracker.sharedInstance.start()
```

Objective-C:
```
[[TQGeoTracker sharedInstance] start];
```

## Stop

To stops the location monitoring, just call the method `stop`:

Swift:
```
TQGeoTracker.sharedInstance.stop()
```

Objective-C:
```
[[TQGeoTracker sharedInstance] stop];
```

## Switch to background

On the `applicationDidEnterBackground` method add:

Swift:
```
TQGeoTracker.sharedInstance.switchToBackgroundMonitoring()
```

Objective-C
```
[[TQGeoTracker sharedInstance] switchToBackgroundMonitoring];
```


## Switch to foreground

On the `applicationWillEnterForeground` method add:

Swift:
```
TQGeoTracker.sharedInstance.switchToForegroundMonitoring()
```

Objective-C
```
[[TQGeoTracker sharedInstance] switchToForegroundMonitoring];
```

## Device Id

If you want to retrieve the device id assigned by the SDK to this device, you need to call the following method:

Swift:
```
TQGeoTracker.sharedInstance.getDeviceId()
```

Objective-C
```
[[TQGeoTracker sharedInstance] getDeviceId];
```

## Foreground Only mode

From version 2.0.2 on, if you don't want to use location when the app is in background, follow these steps:

- Add `Privacy - Location When In Use Usage Description` to your `Info.plist`. The value should be the string that will be shown to the user.

- Change the `configure` method. Now instead of passing each arguments, you use a configuration dictionary, like in the following example:

```objective-c
NSDictionary *TQGConfiguration = @{@"appId": appid,
                                   @"triggerMode": [NSNumber numberWithInt: TriggerModes.Both],
                                   @"environment": [NSNumber numberWithInt: environment],
                                   @"foregroundOnly": @true};


[[TQGeoTracker sharedInstance] configure:TQGConfiguration];

```

Note the `foregroundOnly` key set to true.

- The start should be done every time the app comes to foreground:

```objective-c
- (void)applicationWillEnterForeground:(UIApplication *)application {
    [[TQGeoTracker sharedInstance] start];
}
```

You will notice that on the first time, it will ask location permission to be used only when in use

- Stop TQG when app goes to background (iOS allows the use of location on background even if the permission is only when in use)

```objective-c
- (void)applicationWillResignActive:(UIApplication *)application {
    [[TQGeoTracker sharedInstance] stop];
}
```

Notice that when you go to background, a blue bar will appear for a second saying the app is using the location on background, this happens because iOS is not able to stop the location tracker immediately before going to background.
