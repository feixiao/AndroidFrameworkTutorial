### AudioEffect源码分析

#### Android自带音效 
实现 使用 AudioEffect.ACTION_DISPLAY_AUDIO_EFFECT_CONTROL_PANEL 获取内置音效，参考项目：https://github.com/feixiao/AEQ
```java
android.media.audiofx.BassBoost;         // 重低音
android.media.audiofx.Equalizer;         // 均衡器
android.media.audiofx.PresetReverb;      // 预置混响
android.media.audiofx.Virtualizer;       // 可视化
```
#### BassBoost 分析
```java
// 重低音实现
public class BassBoost extends AudioEffect
```

#### 参考资料
+ [《音效算法集成框架》](https://blog.csdn.net/weixin_41004543/article/details/133707142)
+ [《Android AudioEffect 音效方案》](https://blog.csdn.net/hello_1995/article/details/125303630)