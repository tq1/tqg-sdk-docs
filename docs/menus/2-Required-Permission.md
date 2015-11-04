## Specify Android Permissions

Specify the permissions your application needs, by adding <uses-permission> elements as children of the <manifest> element in AndroidManifest.xml.

You must request the android.permission.WRITE_EXTERNAL_STORAGE permission.
```
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
``

The following permissions are defined in the TQG SDK manifest, and are automatically merged into your app's manifest at build time. You don't need to add them explicitly to your manifest:

 - android.permission.INTERNET - Used by the SDK to comunicate with the TQG API Server.
 - android.permission.ACCESS_NETWORK_STATE - Allows the SDK to access information about networks.
 - android.permission.ACCESS_WIFI_STATE - Allows the SDK to access information about Wi-Fi networks.
 - android.permission.ACCESS_FINE_LOCATION - Allow SDK to access precise user location.