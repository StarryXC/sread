> Thinking

```
WifiManager
WifiConfiguration
WifiInfo
```

> Memory

```
WifiManager wifiManager = (WifiManager) getSystemService(Context.WIFI_SERVICE);
wifiManager.setWifiEnabled(true); // 禁用启动网卡
wifiManager.removeNetwork(1);
WifiConfiguration wifiConfiguration = new WifiConfiguration();
int network = wifiManager.addNetwork(wifiConfiguration);
wifiManager.enableNetwork(1, true);
wifiManager.saveConfiguration();

switch (wifiManager.getWifiState()) { // 网卡状态
    case WifiManager.WIFI_STATE_DISABLED:
        break;
}

WifiInfo wifiInfo = wifiManager.getConnectionInfo();
int ipAddress = wifiInfo.getIpAddress();
String ip = String.format("%d.%d.%d.%d",
        (ipAddress & 0xff),
        (ipAddress >> 8 & 0xff),
        (ipAddress >> 16 & 0xff),
        (ipAddress >> 24 & 0xff));

Enumeration<NetworkInterface> en = NetworkInterface.getNetworkInterfaces();
while (en.hasMoreElements()) {
    NetworkInterface networkInterface = en.nextElement();
    Enumeration<InetAddress> inetAddressEnumeration = networkInterface.getInetAddresses();
    while (inetAddressEnumeration.hasMoreElements()) {
        InetAddress ip = inetAddressEnumeration.nextElement();
        if (!ip.isLoopbackAddress() && InetAddressUtils.isIPv4Address(ip.getHostAddress())) {
            String hostAddress = ip.getHostAddress();
        }
    }
}
```

