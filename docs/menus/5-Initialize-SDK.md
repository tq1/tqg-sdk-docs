To start TQG SDK you must set the desired configuration preference:

 - APP_ID: The application identifier string. 
 - TRIGGER_MODE: Can choose from 3 types of trigger mode - BOTH, LOCAL_ONLY, REMOTE_ONLY
 - TRIGGER_MODE: The environment which the app will run -  PRODUCTION, STAGING, QA, DEVELOPMENT 

This configuration are set by calling the following methods:

```
TQGeoTracker.sharedInstance().configure(getApplicationContext(), <APP_ID>, TQGeoTracker.TriggerMode.<TRIGGER_MODE>, TQGeoTracker.TQEnvironment.<ENVIRONMENT>);
```

You can configure with TRIGGER_MODE and TRIGGER_MODE default values (BOTH AND PRODUCTION):

```
TQGeoTracker.sharedInstance().configure(getApplicationContext(), <APP_ID>);
```

Also you can configure some parameters option (Not required):

  - ACCURACY: Can choose from 4 types of location accuracy - PRIORITY_HIGH_ACCURACY, PRIORITY_BALANCED_POWER_ACCURACY, PRIORITY_LOW_POWER, PRIORITY_NO_POWER. (Default: PRIORITY_HIGH_ACCURACY)
  - CACHE_EXPIRATION: The cache expiration in seconds. (Default: 3600)
  - ZONE_INTERVAL: The zone interval in degrees. (Default: 0.2)
  - LINGER_TIME: The linger time in seconds. (Default: 300)
  - MAX_LINGER_TIME: The max linger time in seconds. (Default: 7200)

This parameters can be set by calling the following methods:

```
TQGeoTracker.sharedInstance().setParameters(TQGeoTracker.Accuracy.<ACCURACY>, <CACHE_EXPIRATION>, <ZONE_INTERVAL>, <LINGER_TIME>, <MAX_LINGER_TIME>)
```

After configure, just call the method `start` to initiate the location tracker.

```
TQGeoTracker.sharedInstance().start(getApplicationContext());
```