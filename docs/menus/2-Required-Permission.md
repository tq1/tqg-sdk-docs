## Specify Android Permissions

The following permissions are defined in the TQG SDK manifest, and are automatically merged into your app's manifest at build time. You don't need to add them explicitly to your manifest:

 - android.permission.INTERNET - Used by the SDK to comunicate with the TQG API Server.
 - android.permission.ACCESS_NETWORK_STATE - Allows the SDK to access information about networks.
 - android.permission.ACCESS_FINE_LOCATION - Allow the SDK to access precise user location.
 - android.permission.ACCESS_COARSE_LOCATION - Allows the SDK to access approximate location.


### Location Permission on Android Versions >= 6

From Android Marshmallow on, permissions for sensitive information access are asked during runtime, so you need to explicitly ask if you want to use them. TQG has methods to do this for you. See example below:

 ```
 if (!TQGeoTracker.sharedInstance().isLocationNotAuthorized(this)) {
        TQGeoTracker.sharedInstance().askForLocationPermission(this);
 }
 ```

This will open a pop-up window asking for permission. The app should handle the permission changed event.

NOTE: The following methods don't need to be called to use the TQG, but you must ensure that the authorization has been allowed by the user:

- ```askForLocationPermission```;
- ```isLocationNotAuthorized```.

### Google Play Services Dependencies

- ```com.google.android.gms:play-services-maps:8.4.0```
- ```com.google.android.gms:play-services-location:8.4.0```
