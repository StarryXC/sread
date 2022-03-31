> Thinking

```
NetworkStatsManager
```

> Memory

```
NetworkStatsManager networkStatsManager = (NetworkStatsManager) getSystemService(Context.NETWORK_STATS_SERVICE);
networkStatsManager.registerUsageCallback(0, "", 0L, new NetworkStatsManager.UsageCallback() {
    @Override
    public void onThresholdReached(int i, String s) { }
});
```

