> Thinking

```
EventBus

```

> Memory

```
https://github.com/greenrobot/EventBus

implementation 'org.greenrobot:eventbus:3.3.1'

EventBus # default register post
Subscribe # threadMode priority

LiveEventBus.get(Event.BIBI_REFRESH)
        .observe(this, androidx.lifecycle.Observer { refresh() })
    LiveEventBus.get(Event.BIBI_REFRESH).post(1)
```
