# android-upnp-discovery
Discovery UPnP devices via SSDP protocol

# Usage

```java
UPnPDiscovery.discoveryDevices(activity, new UPnPDiscovery.OnDiscoveryListener() {
    @Override
    public void OnStart() {
        Log.d("App", "Start");
    }

    @Override
    public void OnFoundNewDevice(UPnPDevice device) {
        Log.d("App", device.toString());
    }

    @Override
    public void OnFinish(HashSet<UPnPDevice> devices) {
        Log.d("App", "Finish");
    }

    @Override
    public void OnError(Exception e) {
        Log.d("App", e.getLocalizedMessage());
    }
});
```
