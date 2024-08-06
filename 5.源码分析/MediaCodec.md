## MediaCodec 介绍

#### 创建 MediaCodec 的⽅式

- 按格式创建 MediaCodec

  ```java
  // 创建解码器
  MediaCodec mediaCodec = MediaCodec.createDecoderByType("video/avc");

  // 创建编码器
  MediaCodec mediaCodec = MediaCodec.createEncoderByType("video/avc");
  ```

- 按 Codec 名字创建 MediaCodec

  ```java
  // OMX.google.h264.decoder：软解码
  // OMX.qcom.video.decoder.avc：硬解码
  MediaCodec createByCodecName(String name)
  ```

#### MediaCodec 创建到 start 的流程

![](./imgs/mediacodec_1.png)

#### 系统

系统中可以存在很多解码器 ， 但能够被应⽤的解码器是根据配置来的,即/system/etc/media_codecs.xml。这个⽂件⼀般由硬件或者系统的⽣产⼚家在编译整个系统的时候提供，⼀般保存在代码的 device/[company]/[codename]⽬录下。

#### 参考资料

- [《自定义媒体组件》](https://source.android.com/docs/core/media/updatable-media?hl=zh-cn)
