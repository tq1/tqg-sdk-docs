On the app's Project/Capabilities enable Background Modes and check the following options:

 - Location Updates: The app keeps users informed of their location, even while it is running in the background.
 - Background Fetch: The app regularly downloads and processes small amounts of content from the network.


 Also, to request the user for location permission, you must add the following key/value in the Info.plist:

 ```
 NSLocationAlwaysUsageDescription/"Your request location usage message"
 ```
