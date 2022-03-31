> Thinking

```

```

> Memory

```
https://github.com/google/ExoPlayer

implementation 'com.google.android.exoplayer:exoplayer:2.13.3'

exoplayer core dash ui

Timeline.Window window = new Timeline.Window();
SimpleExoPlayerView simpleExoPlayerView = null;

BandwidthMeter bandwidthMeter = new DefaultBandwidthMeter();
TrackSelection.Factory videoTrackSelectionFactory =
        new AdaptiveVideoTrackSelection.Factory(bandwidthMeter);
TrackSelector trackSelector =
        new DefaultTrackSelector(videoTrackSelectionFactory);
LoadControl loadControl = new DefaultLoadControl();
SimpleExoPlayer player =
        ExoPlayerFactory.newSimpleInstance(this, trackSelector, loadControl);
simpleExoPlayerView.setPlayer(player);
player.setPlayWhenReady(true);

DefaultBandwidthMeter bandwidthMeter = new DefaultBandwidthMeter();
DataSource.Factory dataSourceFactory = new DefaultDataSourceFactory(this, bandwidthMeter
        , new DefaultHttpDataSourceFactory(Util.getUserAgent(this, "yourApplicationName"), bandwidthMeter));
ExtractorsFactory extractorsFactory = new DefaultExtractorsFactory();
MediaSource videoSource = new ExtractorMediaSource(Uri.parse(VIDEO_URL),
        dataSourceFactory, extractorsFactory, mainHandler, null);
MediaSource videoSource2 = new ExtractorMediaSource(Uri.parse(VIDEO_URL_DEFAULT),
        dataSourceFactory, extractorsFactory, mainHandler, null);
//组合几个视频
ConcatenatingMediaSource concatenatingMediaSource = new ConcatenatingMediaSource(videoSource,videoSource2);
//不停循环
LoopingMediaSource loopingSource = new LoopingMediaSource(concatenatingMediaSource);
player.prepare(loopingSource);

//
DefaultBandwidthMeter bandwidthMeter = new DefaultBandwidthMeter();
// Produces DataSource instances through which media data is loaded.
DataSource.Factory dataSourceFactory = new DefaultDataSourceFactory(this, bandwidthMeter
        , new DefaultHttpDataSourceFactory(Util.getUserAgent(this, "yourApplicationName"), bandwidthMeter));
// Produces Extractor instances for parsing the media data.
ExtractorsFactory extractorsFactory = new DefaultExtractorsFactory();
// This is the MediaSource representing the media to be played.
MediaSource videoSource = new ExtractorMediaSource(Uri.parse(url),
        dataSourceFactory, extractorsFactory, mainHandler, null);

//不停循环
LoopingMediaSource loopingSource = new LoopingMediaSource(videoSource);
SurfaceView sv = (SurfaceView) findViewById(R.id.sv);
player.setVideoSurfaceView(sv);
player.setPlayWhenReady(true);
player.prepare(loopingSource);

//
int playerWindow = player.getCurrentWindowIndex();
playerPosition = C.TIME_UNSET;
Timeline timeline = player.getCurrentTimeline();
if (!timeline.isEmpty() && timeline.getWindow(playerWindow, window).isSeekable) {
    playerPosition = player.getCurrentPosition();
}
player.release();
player = null;
```

