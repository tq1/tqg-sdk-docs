There are two ways of receive a trigger notification: Local and Remote. In the SDK `configure` method, you can choose to receive just one of the two types or both.

| Mode | Description |
|---|---|
| LocalOnly | Only a local trigger will be sent |
| RemoteOnly | Only a remote trigger will be sent to the Geolocation Server |
| Both | A local and a remote trigger will be sent |

## Remote Trigger

The remote trigger send all the trigger data to the TQG server.

## Local Trigger

Local trigger use delegate function to notify the application that a trigger has occurred.
To implement this feature you need to:

  1. Add the protocol to the class declaration.
  2. Implement the the `TQGeoTrackerOnFenceTriggered` method. 
  3. Set the delegate using the `setTriggerDelegate` method


### Add Protocol

You must add the protocol to the class declaration:

Swift:
```
class AppDelegate: ..., TQGeoTrackerDelegate { ... } 
```

Objective-C:
```
@interface MyClass : ... <TQGeoTrackerDelegate>
```


### Implement Protocol Method

To receive the local trigger, you must implement the protocol method `TQGeoTrackerOnFenceTriggered`. This is an implementation example:

Swift:
```
func TQGeoTrackerOnFenceTriggered(tqGeoTracker: TQGeoTracker, trigger: TQTrigger) {
        TQGeoTracker.sharedInstance.log("OnFenceTriggered - fenceName: \(trigger.getFenceName()) fenceId: \(trigger.getFenceId()) type: \(trigger.getEvent())")
        
        if(UIApplication.sharedApplication().applicationState == UIApplicationState.Active) {
            
            let alertController = UIAlertController(title: trigger.getEvent(), message: trigger.getFenceName(), preferredStyle: .Alert)
            
            self.window?.rootViewController?.presentViewController(alertController, animated: true, completion: nil)
            
            
            let delayTime = dispatch_time(DISPATCH_TIME_NOW, Int64(3 * Double(NSEC_PER_SEC)))
            dispatch_after(delayTime, dispatch_get_main_queue()) {

                alertController.dismissViewControllerAnimated(true, completion: nil)
                return
            }
            

        } else {
            
            //Send local notification
            let notification = UILocalNotification()
            notification.fireDate = NSDate()
            notification.alertBody = "fenceName: \(trigger.getFenceName()) fenceId: \(trigger.getFenceId()) type: \(trigger.getEvent())"
            UIApplication.sharedApplication().scheduleLocalNotification(notification)
            
        }
    }
```

Objective-C:
```
-(void)TQGeoTrackerOnFenceTriggered:(TQGeoTracker *)tqGeoTracker trigger:(TQTrigger *)trigger {
    [[TQGeoTracker sharedInstance] log:[NSString stringWithFormat:@"OnFenceTriggered - fenceName: %@ fenceId: %@ type: %@", trigger.getFenceName, trigger.getFenceId, trigger.getEvent]];
    
    if([[UIApplication sharedApplication] applicationState] == UIApplicationStateActive) {

        UIAlertController * alert=   [UIAlertController
                                    alertControllerWithTitle:trigger.getEvent
                                    message:trigger.getFenceName
                                    preferredStyle:UIAlertControllerStyleAlert];

        dispatch_time_t delayTime = dispatch_time(DISPATCH_TIME_NOW, (int64_t)(3 * NSEC_PER_SEC));
        dispatch_after(delayTime, dispatch_get_main_queue(), ^{
            
            [alert dismissViewControllerAnimated:YES completion:nil];
            
        });
        
        
    } else {
        
        //Send local notification
        UILocalNotification *notification = [[UILocalNotification alloc] init];
        notification.fireDate = [[NSDate alloc] init];
        notification.alertBody = [NSString stringWithFormat:@"fenceName: %@ fenceId: %@ type: %@", trigger.getFenceName, trigger.getFenceId, trigger.getEvent];
        [[UIApplication sharedApplication] scheduleLocalNotification: notification];
    }
    
}
```

### Set the Delegate

You must set in the SDK which class will implement the delegate method:

Swift:
```
TQGeoTracker.sharedInstance.setTriggerDelegate(self)
```

Objective-C:
```
[[TQGeoTracker sharedInstance] setTriggerDelegate:self];
```

