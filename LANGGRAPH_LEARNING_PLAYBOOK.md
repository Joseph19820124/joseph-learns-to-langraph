# LangGraph 学习 Playbook
*基于 Google Gemini Fullstack LangGraph Quickstart 的循序渐进学习计划*

## 🎯 项目概述

本项目是基于 [Google Gemini Fullstack LangGraph Quickstart](https://github.com/google-gemini/gemini-fullstack-langgraph-quickstart) 的学习实践，旨在深入理解和掌握使用 LangGraph 构建研究增强型对话AI系统。

### 核心技术栈
- **前端**: React + Vite + TypeScript + Tailwind CSS + Shadcn UI
- **后端**: LangGraph + FastAPI + Google Gemini Models
- **工具**: Google Search API, Redis, PostgreSQL
- **部署**: Docker + Docker Compose

### 系统架构
该项目实现了一个智能研究助手，能够：
1. 接收用户查询
2. 动态生成搜索词条
3. 通过Google Search API进行网络搜索
4. 分析搜索结果，识别知识空白
5. 迭代优化搜索直到获得充分信息
6. 合成最终答案并提供引用来源

## 📚 学习阶段规划

### 阶段 1: 环境准备与基础理解 (第1-2天)

#### 1.1 本地环境搭建
- [ ] 安装 Node.js (推荐 v18+) 和 npm/yarn
- [ ] 安装 Python 3.8+
- [ ] 安装 Docker 和 Docker Compose
- [ ] 配置 Git 环境

#### 1.2 API 密钥准备
- [ ] 获取 Google Gemini API Key
  - 访问 [Google AI Studio](https://makersuite.google.com/)
  - 创建新的API密钥
  - 记录密钥，稍后配置使用
- [ ] 获取 LangSmith API Key (可选，用于调试和监控)
  - 访问 [LangSmith](https://smith.langchain.com/settings)
  - 创建账户并获取API密钥

#### 1.3 理论学习
- [ ] 阅读 [LangGraph 官方文档](https://langchain-ai.github.io/langgraph/)
- [ ] 理解 Agent 架构和状态图概念
- [ ] 学习 RAG (Retrieval-Augmented Generation) 基础

### 阶段 2: 项目克隆与分析 (第3天)

#### 2.1 获取源代码
```bash
# 克隆原始项目
git clone https://github.com/google-gemini/gemini-fullstack-langgraph-quickstart.git
cd gemini-fullstack-langgraph-quickstart

# 分析项目结构
tree -I 'node_modules|__pycache__|*.pyc'
```

#### 2.2 核心文件分析
- [ ] **`backend/src/agent/graph.py`** - LangGraph 主要逻辑
- [ ] **`backend/src/agent/state.py`** - 状态管理
- [ ] **`backend/src/agent/prompts.py`** - 提示词模板
- [ ] **`backend/src/agent/utils.py`** - 工具函数
- [ ] **`frontend/src/App.tsx`** - React 主组件

#### 2.3 数据流理解
研究系统的数据流：
```
用户输入 → 初始查询生成 → 网络搜索 → 结果分析 → 知识空白识别 → 迭代搜索 → 最终答案生成
```

### 阶段 3: 逐步构建后端 (第4-6天)

#### 3.1 Day 4: 基础 Agent 框架
- [ ] 创建基本的 LangGraph 应用结构
- [ ] 实现状态定义 (`state.py`)
- [ ] 创建配置管理 (`configuration.py`)

**实践任务**: 构建一个最简单的"Hello World" LangGraph Agent

#### 3.2 Day 5: 搜索与工具集成
- [ ] 集成 Google Search API
- [ ] 实现搜索工具 (`tools_and_schemas.py`)
- [ ] 创建查询生成节点

**实践任务**: 实现能够接收用户输入并进行基础搜索的功能

#### 3.3 Day 6: 核心 Agent 逻辑
- [ ] 实现完整的 graph 结构
- [ ] 添加反思和迭代逻辑
- [ ] 优化提示词设计

**实践任务**: 完成核心 Agent 的搜索-分析-迭代循环

### 阶段 4: 前端开发 (第7-8天)

#### 4.1 Day 7: React 应用基础
- [ ] 设置 Vite + React + TypeScript 环境
- [ ] 配置 Tailwind CSS 和 Shadcn UI
- [ ] 创建基本的聊天界面

#### 4.2 Day 8: 前后端集成
- [ ] 实现与 LangGraph API 的通信
- [ ] 添加实时流式响应
- [ ] 优化用户界面和体验

### 阶段 5: 高级功能与优化 (第9-10天)

#### 5.1 Day 9: 功能增强
- [ ] 添加对话历史管理
- [ ] 实现引用和来源展示
- [ ] 添加错误处理和重试机制

#### 5.2 Day 10: 部署与测试
- [ ] 配置 Docker 容器化
- [ ] 设置 docker-compose 部署
- [ ] 进行端到端测试

## 🛠 实践检查点

### 检查点 1: 基础环境 (第2天结束)
- [ ] 成功运行原始项目
- [ ] 理解 LangGraph 基本概念
- [ ] API 密钥配置完成

### 检查点 2: 后端理解 (第6天结束)
- [ ] 独立构建基础 Agent
- [ ] 实现搜索功能集成
- [ ] 理解状态图工作流程

### 检查点 3: 全栈应用 (第8天结束)
- [ ] 前后端成功通信
- [ ] 基本聊天功能可用
- [ ] 界面响应正常

### 检查点 4: 项目完成 (第10天结束)
- [ ] 完整功能实现
- [ ] Docker 部署成功
- [ ] 文档和代码注释完整

## 🔧 开发工具和资源

### 必备工具
- **IDE**: VS Code (推荐插件: Python, TypeScript, Tailwind CSS)
- **API 测试**: Postman 或 Insomnia
- **数据库管理**: pgAdmin (PostgreSQL) 或 Redis Insight
- **版本控制**: Git + GitHub

### 学习资源
- [LangGraph 文档](https://langchain-ai.github.io/langgraph/)
- [Google Gemini API 文档](https://ai.google.dev/docs)
- [React + TypeScript 指南](https://react-typescript-cheatsheet.netlify.app/)
- [FastAPI 文档](https://fastapi.tiangolo.com/)

## 📝 日志记录模板

每天学习结束后，请在此记录学习进度：

### Day X 学习日志
- **学习内容**: 
- **完成任务**: 
- **遇到问题**: 
- **解决方案**: 
- **明日计划**: 

## 🚀 进阶挑战

完成基础学习后的扩展挑战：

1. **多模态集成**: 添加图像搜索和分析功能
2. **知识图谱**: 集成结构化知识存储
3. **个性化**: 实现用户偏好学习
4. **性能优化**: 实现搜索缓存和并行处理
5. **部署扩展**: 添加 Kubernetes 部署配置

## 📞 获取帮助

遇到问题时的求助渠道：
- GitHub Issues (本项目)
- LangGraph Discord 社区
- Stack Overflow (标签: langgraph, langchain)
- Google Gemini 开发者论坛

---

**祝您学习愉快！记住：实践出真知，多动手，多思考！** 🎉
