# Agent的基本架构

agent随着大模型技术的演进逐步收到越来越多的的关注，其Agent的基本架构总体看仍然符合此前的技术路线。

![agent基本架构](https://github.com/xiangyuliu/material_arrangement/blob/main/sources/image/agent%E9%80%9A%E7%94%A8%E6%9E%B6%E6%9E%84%E5%8F%8A%E5%85%B6%E7%BB%84%E4%BB%B6-2025-01-14-1041.png)

## 执行状态


![执行状态](https://github.com/xiangyuliu/material_arrangement/blob/main/sources/image/%E5%91%A8%E6%9C%9F%E6%89%A7%E8%A1%8C%E7%A4%BA%E6%84%8F%E5%9B%BE-2025-01-14-1041.png)


## Agent 框架的控制粒度
### 复杂度取舍
![复杂度平衡](https://github.com/xiangyuliu/material_arrangement/blob/main/sources/image/%E5%A4%8D%E6%9D%82%E5%BA%A6-2025-01-14-1041.png)



### 控制粒度
![控制粒度](https://github.com/xiangyuliu/material_arrangement/blob/main/sources/image/%E4%B8%8D%E5%90%8C%E6%8E%A7%E5%88%B6%E7%A8%8B%E5%BA%A6-2025-01-14-1041.png)


## 常见框架
常见的框架非常多，简单介绍autogen和langgraph。因为两者都是非常具有代表性的框架结构。

### autogen
**设计理念——对话即一切** 一切以对话为核心，通过对话机制实现功能。这是autogen的核心设计逻辑。

*1.Multi-agent的发言交由group chat manager进行管理*
*2.具体管理的方式有很多选项方式，比如llm判断，轮转等等*


![基本角色](https://github.com/xiangyuliu/material_arrangement/blob/main/sources/image/autogen%E5%9F%BA%E6%9C%AC%E8%A7%92%E8%89%B2-2025-01-14-1041.png)

