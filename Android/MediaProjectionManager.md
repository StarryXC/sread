> Thinking

```
MediaProjectionManager


```

> Memory

```
MediaProjectionManager mediaProjectionManager = (MediaProjectionManager) getSystemService(Context.MEDIA_PROJECTION_SERVICE);
Intent intent = mediaProjectionManager.createScreenCaptureIntent();
startActivityForResult(intent, 100);

MediaProjection mediaProjection = mediaProjectionManager.getMediaProjection(resultCode, data);
MediaCodec mediaCodec = MediaCodec.createEncoderByType("video/avc");
MediaFormat mediaFormat = MediaFormat.createVideoFormat("video/avc", 720, 1280);
mediaFormat.setInteger(MediaFormat.KEY_COLOR_FORMAT, MediaCodecInfo.CodecCapabilities.COLOR_FormatSurface);
mediaFormat.setInteger(MediaFormat.KEY_BIT_RATE, 400_000);
mediaFormat.setInteger(MediaFormat.KEY_FRAME_RATE, 15);
mediaFormat.setInteger(MediaFormat.KEY_I_FRAME_INTERVAL, 2);
mediaCodec.configure(mediaFormat, null, null, MediaCodec.CONFIGURE_FLAG_ENCODE);
Surface surface = mediaCodec.createInputSurface();
VirtualDisplay virtualDisplay = mediaProjection.createVirtualDisplay(
        "screen-codec",
        720, 1280, 1,
        DisplayManager.VIRTUAL_DISPLAY_FLAG_PUBLIC,surface, null, null);

mediaCodec.start();
MediaCodec.BufferInfo bufferInfo = new MediaCodec.BufferInfo();
long time = System.currentTimeMillis();

long startTime = bufferInfo.presentationTimeUs / 1000;
OutputStream outputStream = new FileOutputStream("");
int index = mediaCodec.dequeueOutputBuffer(bufferInfo, 100_000);// 微妙
if (index >= 0) {
    if (System.currentTimeMillis() - time >= 2000) { // 2s 关键帧
        Bundle bundle = new Bundle();
        bundle.putInt(MediaCodec.PARAMETER_KEY_REQUEST_SYNC_FRAME, 0);
        mediaCodec.setParameters(bundle);
        time = System.currentTimeMillis();
    }
    ByteBuffer byteBuffer = mediaCodec.getOutputBuffer(index);
    byte[] outData = new byte[bufferInfo.size];
    byteBuffer.get(outData);
    long duration = bufferInfo.presentationTimeUs / 1000 - startTime;
    outputStream.write(outData);
    outputStream.write('\n');
    mediaCodec.releaseOutputBuffer(index, false);
}


```

