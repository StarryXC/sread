> Thinking

```
LocationManager
Geocoder
```

> Memory

```
Geocoder geocoder = new Geocoder(context);
List<Address> addressList = geocoder.getFromLocation(40.714, -73.961, 1);

LocationManager locationManager = (LocationManager) context.getSystemService(Context.LOCATION_SERVICE);
if (ActivityCompat.checkSelfPermission(context, Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED
        && ActivityCompat.checkSelfPermission(context, Manifest.permission.ACCESS_COARSE_LOCATION) != PackageManager.PERMISSION_GRANTED) {
}
locationManager.getAllProviders();

Criteria criteria = new Criteria(); // 设置查询条件 查询Location Provider
criteria.setAccuracy(Criteria.ACCURACY_FINE);
criteria.setPowerRequirement(Criteria.POWER_LOW);
criteria.setAltitudeRequired(false);
criteria.setSpeedRequired(false);
criteria.setCostAllowed(false);
locationManager.getBestProvider(criteria, false);

locationManager.requestLocationUpdates(LocationManager.GPS_PROVIDER, 5000, 5000, new LocationListener() {
    @Override
    public void onLocationChanged(Location location) { }
    @Override
    public void onStatusChanged(String provider, int status, Bundle extras) { }
    @Override
    public void onProviderEnabled(String provider) { }
    @Override
    public void onProviderDisabled(String provider) { }
});

http://maps.googleapis.com/maps/api/geocode/json?
    address=sdd
    bounds=34.34,-118|34.23,-118.23
    sensor=false
    latlng=40.12,-73.we
    region=es
```

