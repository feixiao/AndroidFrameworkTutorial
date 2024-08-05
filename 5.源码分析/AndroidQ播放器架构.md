## Android Q 播放器架构

Android 10 之后引入专用的 C2 架构（用来代理 OMX IL 架构），C2 相比 OMX 更加灵活，支持更多功能。
![](./imgs/player.png)

#### 解码数据流向

1. 音乐 APP 调用 MediaPlayer 接口播放音乐，并将原始音乐文件的 fd 传给 MediaPlayService
2. MediaPlayService 调用 NuPlayer，NuPlayer 使用 MediaExtractor 对该文件进行解析，识别音轨，歌曲信息，播放时长等。
3. NuPlayer 使用 MediaExtractor 提取数据，将数据送给 MediaCodec 的 Input Buffer。
4. MediaCodec 使用软解码 SW decoder，最终解码后是 PCM 数据，放到 Output Buffer。
5. NuPlayer 从 Output Buffer 取数据，再通过 AudioTrack 将音频数据送给 AudioFlinger。
6. AudioFlinger 再通过 ALSA 驱动写到 DSP，DSP 处理后转成模拟信号播放出来。
   ![](./imgs/audio_data_flow.png)

#### 视频解码流向

1. 视频 APP 调用 MediaPlayer 接口播放视频，并将原始视频文件的 fd 传给 MediaPlayService。
2. MediaPlayService 调用 NuPlayer，NuPlayer 使用 MediaExtractor 对该文件进行解析，识别音轨，歌曲信息，播放时长等。
3. NuPlayer 使用 MediaExtractor 提取数据，将数据送给 MediaCodec 的 Input Buffer。
4. MediaCodec 使用软解码 SW decoder 或硬解码 VPU 解码，最终解码后是 YUV 数据，放到 Output Buffer。
5. NuPlayer 从 Output Buffer 取数据，再通过 Surface 将音频数据送给 SurfaceFlinger。
6. SurfaceFlinger 再通过 HW Composer 将数据推送到 DPU 进行渲染，之后再推到屏幕显示。
   ![](./imgs/video_data_flow.png)
