# Android-uPnP-Discovery
Discover UPnP devices via SSDP (Simple Service Discovery Protocol) on the current WiFi network

##How:

⋅⋅*Send M-SEARCH request via Multicast UDP
⋅⋅*Receive Unicast UDP response from compatile devices

# Installation
## Gradle
```text
compile 'com.github.custanator:upnpdiscovery:1.0.1'
```

# Usage
## Basically usage
Search all devices (M-SEARCH ST: ssdp:all)

```java
UPnPDiscovery.discoveryDevices(activity, new UPnPDiscovery.OnDiscoveryListener() {
    @Override
    public void OnStart() {
        Log.d("UPnPDiscovery", "Starting discovery");
    }

    @Override
    public void OnFoundNewDevice(UPnPDevice device) {
        Log.d("UPnPDiscovery", "Found new device: " + device.toString());
        // String friendlyName = device.getFriendlyName();
        // ... see UPnPDevice description below
    }

    @Override
    public void OnFinish(HashSet<UPnPDevice> devices) {
        Log.d("UPnPDiscovery", "Finish discovery");
    }

    @Override
    public void OnError(Exception e) {
        Log.d("UPnPDiscovery", "Error: " + e.getLocalizedMessage());
    }
});
```

## Extended usage
For custom query use:

```java
String customQuery = "M-SEARCH * HTTP/1.1" + "\r\n" +
        "HOST: 239.255.255.250:1900" + "\r\n" +
        "MAN: \"ssdp:discover\"" + "\r\n" +
        "MX: 1"+ "\r\n" +
        //"ST: urn:schemas-upnp-org:service:AVTransport:1" + "\r\n" + // Use for Sonos
        //"ST: urn:schemas-upnp-org:device:InternetGatewayDevice:1" + "\r\n" + // Use for Routers
        "ST: ssdp:all" + "\r\n" + // Use this for all UPnP Devices (DEFAULT)
        "\r\n";
int customPort = 1900;
String customAddress = "239.255.255.250";

UPnPDiscovery.discoveryDevices(this, new UPnPDiscovery.OnDiscoveryListener() {
    @Override
    public void OnStart() {
        Log.d("UPnPDiscovery", "Starting discovery");
    }

    @Override
    public void OnFoundNewDevice(UPnPDevice device) {
        Log.d("UPnPDiscovery", "Found new device: " + device.toString());
        // String friendlyName = device.getFriendlyName();
        // ... see UPnPDevice description below
    }

    @Override
    public void OnFinish(HashSet<UPnPDevice> devices) {
        Log.d("UPnPDiscovery", "Finish discovery");
    }

    @Override
    public void OnError(Exception e) {
        Log.d("UPnPDiscovery", "Error: " + e.getLocalizedMessage());
    }
}, customQuery, customAddress, customPort);
```

## Methods
UPNPDevice object has methods:

```java
    public String getHostAddress();
    public String getHeader();
    public String getST();
    public String getUSN();
    public String getServer();
    public String getLocation();
    public String getDescriptionXML();
    public String getDeviceType();
    public String getFriendlyName();
    public String getPresentationURL();
    public String getSerialNumber();
    public String getModelName();
    public String getModelNumber();
    public String getModelURL();
    public String getManufacturer();
    public String getManufacturerURL();
    public String getUDN();
    public String getURLBase();
    
    // Return all params 
    public String toString();
```

# Links
https://en.wikipedia.org/wiki/Universal_Plug_and_Play
https://en.wikipedia.org/wiki/Simple_Service_Discovery_Protocol
https://tools.ietf.org/html/draft-cai-ssdp-v1-03#section-2.2.1
http://www.upnp.org/specs/arch/UPnP-arch-DeviceArchitecture-v1.1.pdf
https://github.com/berndverst/android-ssdp
