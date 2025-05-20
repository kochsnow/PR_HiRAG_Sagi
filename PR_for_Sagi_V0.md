# Sagi: 开源AI Agent框架的系统架构与功能解析

在大模型应用快速发展的背景下，Sagi作为一个新开源的AI Agent框架，提供了一套结构化的解决方案，专注于增强AI系统的深度思考和知识处理能力。本文将介绍Sagi的核心设计理念和技术特点。

## 双阶段工作流架构

Sagi采用了一种结构化的工作流架构，将复杂任务处理分为两个主要阶段：

- **计划生成阶段**：
  - 任务分析：识别已知信息与需要获取的信息
  - 事实分类：区分显式陈述的事实、系统已知的事实、需要检索的信息以及需要推导的信息
  - 步骤规划：基于分析制定详细的执行计划

- **计划执行阶段**：
  - 任务分流：通过Triage Agent将子任务分配给专门的工具代理
  - 工具集成：整合文件检索、代码执行和网络搜索等功能模块
  - 执行监控：实时跟踪计划执行状态，支持动态调整

这种架构设计使Sagi能够更系统地处理需要多步骤推理的复杂任务，提高解决问题的效率和质量。

## GraphRAG知识检索技术

Sagi集成了GraphRAG技术来增强知识检索能力：

- **图结构知识表示**：将知识库内容组织为图结构，保留信息间的关联关系
- **层次化检索机制**：支持从概念层级到具体细节的多层次检索
- **关系感知**：在检索过程中考虑实体间的语义关系，提高结果相关性

相比传统的向量检索方法，GraphRAG能够更好地处理需要上下文理解和关联推理的复杂查询。

## MCP协议集成

Sagi实现了Model Context Protocol（MCP）标准，这是一种由Anthropic提出的模型与外部工具交互协议：

- **统一接口**：提供标准化的工具调用接口，简化集成流程
- **可扩展性**：开发者可以遵循MCP规范轻松扩展新功能
- **工具生态**：能够连接到现有的MCP服务生态系统

MCP的集成使Sagi能够灵活地利用外部工具和服务，增强其处理能力范围。

## 系统组件结构

Sagi的核心组件包括：

1. **Plan Manager**：管理计划状态和历史，支持多轮对话中的计划追踪
2. **Agents集合**：
   - Fact Analyzer：分析任务中的事实类型
   - Planner：生成执行计划
   - Reflection Agent：评估执行情况并调整计划
   - Tool Agents：专门执行特定任务的代理组件
3. **MCP Servers**：提供工具服务的接口层
4. **文档数据库**：支持高效的知识存储和检索

## 部署与使用

Sagi提供了基于Docker的简单部署方案：

```bash
# 克隆仓库
git clone [https://github.com/Kasma-Inc/Sagi.git](https://github.com/Kasma-Inc/Sagi.git)
cd Sagi
git submodule update --init --recursive

# 环境配置
cp .env.example .env
# 设置API密钥和其他配置

# 构建Docker容器
chmod +x dev/setup_dc.sh
./dev/setup_dc.sh

# 安装依赖并启动
pip install -e .
python cli.py
```