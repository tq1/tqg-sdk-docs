The TQG SDK have two public fragments that can be used by the app for debug purpose.

## Debug Map

The `DebugMapFragment` is a Open Street Map which shows the user location, fences and zone. The fragment can be use as the following example:

```
DebugMapFragment fragmentMap = new DebugMapFragment();
FragmentManager fragmentManager = getFragmentManager();
FragmentTransaction fragmentTransaction = fragmentManager.beginTransaction();
fragmentTransaction.replace(R.id.map_fragment_container, fragmentMap);
fragmentTransaction.commit();
```

To refresh the map and synchronize the fences with the database, you should call the following method:

```
fragmentMap.refreshMap();
```


## Debug Log

The `LogFragment` is a fragment tha can be used to monitor all the SDK logs. This is helpful for debug purpose. The fragment can be use as the following example:

```
LogFragment fragmentLog = new LogFragment();
FragmentManager fragmentLogManager = getFragmentManager();
FragmentTransaction fragmentTransaction = fragmentLogManager.beginTransaction();
fragmentTransaction.replace(R.id.log_container, fragmentLog);
fragmentTransaction.commit();
```

To refresh the log and synchronize the messages with the database, you should call the following method:

```
fragmentLog.refreshLog();
```