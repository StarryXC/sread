> Thinking

```
BluetoothManager
监听蓝牙状态变化 获取蓝牙状态
```

> Memory

```
BluetoothAdapter bluetoothAdapter = BluetoothAdapter.getDefaultAdapter(); // 无蓝牙 null
if (bluetoothAdapter != null) {
    bluetoothAdapter.isDiscovering(); bluetoothAdapter.startDiscovery(); bluetoothAdapter.cancelDiscovery();
    bluetoothAdapter.isEnabled(); bluetoothAdapter.enable(); bluetoothAdapter.disable();// 蓝牙启用
    Set<BluetoothDevice> bondedDevices = bluetoothAdapter.getBondedDevices(); // 已配对的蓝牙适配器
    bondedDevices.iterator().next().getAddress();
    bondedDevices.iterator().next().getAddress();
}

Intent intent = new Intent(BluetoothDevice.ACTION_FOUND);
BluetoothDevice bluetoothDevice = intent.getParcelableExtra(BluetoothDevice.EXTRA_DEVICE);

// 提示longue开启蓝牙 未开启时使用
Intent intent = new Intent(BluetoothAdapter.ACTION_REQUEST_ENABLE);

// 修改蓝牙设备可见性
Intent intent = new Intent(BluetoothAdapter.ACTION_REQUEST_DISCOVERABLE);
intent.putExtra(BluetoothAdapter.EXTRA_DISCOVERABLE_DURATION, 500); // 可见状态持续时间

```
