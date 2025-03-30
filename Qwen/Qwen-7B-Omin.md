# Qwen-7B-Omin

# 引言

千问最近有点卷。发布了7B的端到端全模态的模型。这个模型在评测和使用上面满堂彩。空余时间看了一下对应的技术报告，顺手做一个笔记。

引述一下他们的总结：

_Qwen2.5-Omni 是一个统一的模型，旨在理解和生成多种模态，包括文本和实时语音。为了增强视频集成，我们引入了一种新的位置嵌入方法，称为 TMRoPE，它对齐音频和视频的时间。我们的 Thinker-Talker 框架支持实时语音生成，同时最大限度地减少不同模态之间的干扰。此外，我们还采用了块级音频/视觉编码和滑动窗口机制进行代码到波形的生成。这种创新模型在复杂的音频-视频交互和带有情感上下文的语音对话中表现出色。_

_综合评估表明，Qwen2.5-Omni 在性能上优于类似规模的单模态模型，特别是在遵循语音命令方面，并且在多模态任务中达到了最先进的水平。在模型开发过程中，我们确定了几个关键问题，这些问题在以前的学术研究中经常被研究人员忽视，例如视频 OCR 和音频-视频协作理解。应对这些挑战需要学术界和工业界的合作，特别是在构建全面的评估基准和研究数据集方面。我们相信 Qwen2.5-Omni 代表了向通用人工智能 (AGI) 迈出的重要一步。我们的未来目标包括开发一个更强大、更快的模型，并在各种模态（如图像、视频和音乐）上扩展输出能力。_

**核心有几个点：**

1.  **编码方式上面采用TMRoPE，统一文本、音频和视频的编码。此项技术在此前的QWen 2.5 VL中已经使用。其3D编码能够实现图像全尺寸时间上的绝对编码。**
    
2.  **采用了thinker-talker的架构模式，能够很好的进行理解和语音生成。**
    
3.  **为了提升效率，采用了块的预填充和滑动窗口的注意力机制。**
    
4.  **细节技术非常好：比如音频和视频向量的拼合；talker阶段对thinker的文本token的采样等技术；训练过程中对自然语言提示替换了Qwen2-Audio中的分层标签等。**
    

# 概览

![QWen-7B-总论.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/4EZlwoEG6g1YlxAY/img/03a8a3e2-ca75-45be-a01b-7202024f5a9c.png)

# 模型结构

![QWen-7B-模型结构.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/4EZlwoEG6g1YlxAY/img/d64b4ee9-62bd-4a05-a0de-93429a680499.png)

# 感知

![QWen-7B-感知.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/4EZlwoEG6g1YlxAY/img/a27f3180-ec4e-41ee-a040-df8b33128994.png)

# 生成

![QWen-7B-生成.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/4EZlwoEG6g1YlxAY/img/194d2a6c-7727-4a89-b4ad-d1e3437f0651.png)

# 流式性能优化

![QWen-7B-流式.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/4EZlwoEG6g1YlxAY/img/d37b0a7b-9859-4dd5-bcfb-49f0e4965784.png)

# 预训练

![QWen-7B-预训练.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/4EZlwoEG6g1YlxAY/img/d20a5e3f-1cb8-422b-a5b9-7fa7af5c9949.png)

# 后训练

![QWen-7B-后训练.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/4EZlwoEG6g1YlxAY/img/d4943ebc-23bd-4d9d-9c6f-5907b9914c1f.png)