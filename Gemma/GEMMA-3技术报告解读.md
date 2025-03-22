# GEMMA-3技术报告解读

## 前言

GEMMA3自发布以来引起了广泛关注，其在较小的参数规模（27B）实现了接近DeepSeek-v3接近的能力，对此非常值得关注。

个人对其技术报告进行了分析，个人觉得其核心如下几个方面：

1.  _**模型蒸馏——使用好的蒸馏方式对更大规模模型进行蒸馏，压缩模型规模。**_
    
2.  _**模型经过多个阶段的微调，对齐了人类偏好、数学推理能力和代码生成能力。尤其是其在强化学习阶段的多种奖励函数的设计有很大的帮助。**_
    
3.  _**多模态中视觉编码能力的优化——固定窗口大小，针对不规则图片的resize和窗口覆盖**_
    
4.  _**值得关注的性能优化的方式：**_
    
    1.  _**使用分层注意力机制：局部注意力层和全局注意力层的五比一配置，有效降低KV缓存的使用。**_
        
    2.  _**视觉编码器在推理阶段总块数的控制。**_
        

## 内容

### 模型结构

![GEMMA-3模型架构.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/Mp7ld84QKozxlBQN/img/18970043-4266-4a30-bf9a-e088eef03f10.png)

![GEMMA-3模型架构-视觉模态.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/Mp7ld84QKozxlBQN/img/df07d30d-b127-40d4-8ce1-7822760f5f31.png)

### 训练

![GEMMA-3训练步骤-总体.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/Mp7ld84QKozxlBQN/img/aedfff3e-2e89-413e-b134-b4860764ae07.png)

![GEMMA-3训练步骤-预训练.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/Mp7ld84QKozxlBQN/img/c9064ccf-9284-4e2e-b29d-64f39bc7b539.png)

![GEMMA-3训练步骤——量化感知训练（QAT）.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/Mp7ld84QKozxlBQN/img/4fed4efe-fc50-44de-b41f-7eeb4bd9ace0.png)

![GEMMA-3训练步骤——计算基础设施.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/Mp7ld84QKozxlBQN/img/b884b13e-6a0a-4159-b31e-22518248daa7.png)

![GEMMA-3指令微调.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/Mp7ld84QKozxlBQN/img/536a0930-7396-45f0-b456-c905a23418e2.png)