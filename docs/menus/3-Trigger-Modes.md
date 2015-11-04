There are two ways of receive a trigger notification: Local and Remote. In the SDK `configure` method, you can choose to receive just one of the two types or both.

## Local Trigger

Local trigger use broadcast to notify the application that a trigger has occurred.
To implement this feature you need to:

  1. Register a receiver in the `AndroidManifest.xml` file.
  2. Extend a BroadcastReceiver class and implement the `onReceive()` method. 


### Register a receiver

To register a receiver you need to add the following lines in the `AndroidManifest.xml` file:

```
<receiver
    android:name=".MyReceiver"
    android:exported="true" >
    <intent-filter>
        <action android:name="com.taqtile.tqgeolocationsdk.LOCAL_TRIGGER">
        </action>
    </intent-filter>
</receiver>
```

`MyReceiver` is the name of the class that extends BroadcastReceiver and which will implement the `onReceive` method.

### Extend BroadcastReceiver class

To receive the local trigger, you must extend a BroadcastReceiver class and implement the `onReceive()` method. This is a example of a class that receive the Intent broadcast in the `onReceive` method:

```
public class MyReceiver extends BroadcastReceiver {
    public MyReceiver() {
    }

    @Override
    public void onReceive(Context context, Intent intent) {
        // This method is called when the BroadcastReceiver is receiving
        // an Intent broadcast.
        String deviceId = intent.getStringExtra("decideId");
        String fenceId = intent.getStringExtra("fenceId");
        int timestamp = intent.getIntExtra("timestamp", 0);
        String fenceName = intent.getStringExtra("fenceName");
        String event = intent.getStringExtra("event");
    }
}
```

The Intent broadcast has the following extra fields:

 - `deviceId`: (String) - The unique device id.
 - `fenceId`: (String) - The fence id in which the trigger has ococcurred.
 - `timestamp`: (int) - The unix time stamp
 - `fenceName`: (String) - The fence name in which the trigger has ococcurred.
 - `event`: (String) - The trigger type: enter, exit or linger.


## Remote Trigger

The remote trigger send all the trigger data to the TQG server.

