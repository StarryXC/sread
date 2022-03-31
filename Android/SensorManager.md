> Thinking

```
SensorManager
Sensor
SensorListener
SensorEvent
```

> Memory

```
SensorManager sensorManager = (SensorManager) getSystemService(Context.SENSOR_SERVICE);
sensorManager.getSensorList(Sensor.TYPE_ALL);

Sensor sensor = sensorManager.getDefaultSensor(Sensor.TYPE_ACCELEROMETER); // 类型默认传感器
sensor.getName(); // 名称
sensor.getVendor();//制造商
sensor.getResolution();//
sensor.getPower();//功率
switch (sensor.getType()) { // 传感器种类
    case Sensor.TYPE_LIGHT: // 光线传感器
    case Sensor.TYPE_ACCELEROMETER: // 加速度 重力 陀螺仪
    动作传感器
    位置传感器 方向 磁力
    环境传感器 温度 压力 亮度
}

SensorEventListener sensorEventListener = new SensorEventListener() {
    @Override
    public void onSensorChanged(SensorEvent sensorEvent) {
        float x = sensorEvent.values[0];
        float y = sensorEvent.values[1];
        float z = sensorEvent.values[2];
        Math.sqrt(x * x + y * y + z * z);
        Sensor sensor = sensorEvent.sensor;
        sensorEvent.timestamp;
        sensorEvent.accuracy;
    }

    @Override
    public void onAccuracyChanged(Sensor sensor, int i) { }
};
// 传感器采样率 设置低采样率 省电
SensorManager.SENSOR_DELAY_NORMAL; // 200_000 微妙
SensorManager.SENSOR_DELAY_UI;// 60_000 微妙
SensorManager.SENSOR_DELAY_GAME;// 20_000 微妙
SensorManager.SENSOR_DELAY_FASTEST;// 0微妙
sensorManager.registerListener(sensorEventListener, sensor, SensorManager.SENSOR_DELAY_GAME);
sensorManager.unregisterListener(sensorEventListener);
```

