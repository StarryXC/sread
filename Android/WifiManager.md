> Thinking

```
WifiConfiguration
wifiManager.isWifiEnabled()
wifiManager.removeNetwork(foundNetworkID);
      wifiManager.saveConfiguration();
wifiManager.addNetwork(config);
wifiManager.enableNetwork(networkId
wifiManager.saveConfiguration();
```

> Memory

```
WifiManager wifiManager = (WifiManager) context
				.getSystemService(context.WIFI_SERVICE);
		WifiInfo wifiInfo = wifiManager.getConnectionInfo();
		int ipAddress = wifiInfo.getIpAddress();
		String ip = String.format("%d.%d.%d.%d", (ipAddress & 0xff),
				(ipAddress >> 8 & 0xff), (ipAddress >> 16 & 0xff),
				(ipAddress >> 24 & 0xff));
		return ip;

Enumeration<NetworkInterface> en = NetworkInterface.getNetworkInterfaces();
while (en.hasMoreElements())
{
	NetworkInterface nif = en.nextElement();//
	Enumeration<InetAddress> inet = nif.getInetAddresses();
	while (inet.hasMoreElements())
	{
		InetAddress ip = inet.nextElement();
		if (!ip.isLoopbackAddress()
				&& InetAddressUtils.isIPv4Address(ip
				.getHostAddress()))
		{
			return ipaddress = ip.getHostAddress();
		}
	}
}	
```

