
## 1. Extract encoded data from file & feed to decoder

Ask for (dequeue) free buffer from codec (It's a direct ByteBuffer).
Fill the data to that buffer from extract.
Return the filled data buffer back to codec (queue).

```java
int bufferIndex = decoder.dequeueInputBuffer(TIMEOUT_SEC);

// only get the buffer if `bufferIndex` is valid
ByteBuffer buffer = decoder.getInputBuffer(bufferIndex);

// fill the buffer with encoded sample from file
int sampleSize = extractor.readSampleData(bufferIndex, 0);
long presentationTime = extractor.getSampleTime();
int sampleFlags = extractor.getSampleFlags();

boolean isEos = !extractor.advance();

// only queue the `inputBuffer` to codec if valid
decoder.queueInputBuffer(buffer, 0, sampleSize, presentationTime, sampleFlags);
```


## 2. Poll out frame from decoder & feed to encoder

```java
int bufferIndex = decoder.dequeueOutputBuffer(bufferInfo, TIMEOUT_SEC);

// only processing if `bufferIndex` is valid
// ByteBuffer buffer = decoder.getOutputBuffer(bufferIndex);

boolean render = bufferInfo.size != 0;

decoder.releaseOutputBuffer(bufferIndex, render); // render = true will send the buffer to output surface => the surface will release the buffer back to codec when it is no longer used.

// when we config the decoder, we pass the `surface` to the `MediaCodec#config` method. So when ever we have new decoded frame from decoder, we will receive it from `android.graphics.SurfaceTexture.OnFrameAvailableListener`

// SurfaceTexture st = new SurfaceTexture(oesTexId);
// Surface surface = new Surface(st);


```

## 3. Poll frames from encoder & send them to muxer


```java
int bufferIndex = encoder.dequeOutputBuffer(bufferInfo, TIMEOUT_SEC);

// Only processing if `bufferIndex` is valid
ByteBuffer buffer = encoder.getOutputBuffer(bufferIndex);

// only write sample to muxer if bufferIndo.size != 0
muxer.writeSampleData(videoOrAudioTrack, buffer, bufferInfo);

encoder.releaseOutputBuffer(bufferIndex, false);

```
