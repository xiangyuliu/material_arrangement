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

具体使用方式可以参看官方文档


![基本角色](https://github.com/xiangyuliu/material_arrangement/blob/main/sources/image/autogen%E5%9F%BA%E6%9C%AC%E8%A7%92%E8%89%B2-2025-01-14-1041.png)


### langraph
**设计理念而言langgraph提供底层的控制能力**，控制权交由用户侧（开发者），基于用户侧更强的控制能力。

作为一个非常底层的框架，它提供了对应用程序流和状态的细粒度控制，这对于创建可靠的代理至关重要。此外，LangGraph 包括内置持久性，支持高级的人参与的循环和内存功能。

![langgraph基本构成](https://github.com/xiangyuliu/material_arrangement/blob/main/sources/image/%E6%9E%84%E6%88%90graph.png)



##  Qwen-Agent
Qwen-Agent主要服务于通义的大模型，提供了基本的一些能力,围绕模型做基本的模型能力封装，与autogen和langgraph等相比较而言，仍然略显简陋。

***Qwen-Agent 的主要功能***

*	•	指令遵循：Qwen-Agent 能理解和执行用户的指令。

	•	工具使用：支持智能体调用外部工具完成任务。

	•	记忆能力：Qwen-Agent 具备记忆上下文的能力，能在对话中保持状态。

	•	函数调用：支持智能体调用预定义的函数或 API。

	•	代码解释器：内置代码解释器，支持智能体执行和解释代码。

	•	多代理框架：支持构建和管理多个智能代理。*

***Qwen-Agent 的技术原理***

*	•	大语言模型（LLM）：基于大型预训练语言模型，如 Qwen，处理复杂的语言任务。

	•	工具集成：集成各种工具，包括 API、脚本或外部程序，智能体。

	•	智能代理架构：用智能代理架构，智能体能继承自Agent类，实现具体的应用逻辑。

	•	RAG 算法：用 RAG 算法处理长文档，将文档分割成小块，保留最相关的部分，提升上下文处理能力。*



