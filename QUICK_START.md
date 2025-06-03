# 快速开始指南

## 🚀 立即开始实验

### 第一步：环境准备

#### 1. 克隆原始项目
```bash
# 在你的工作目录下
git clone https://github.com/google-gemini/gemini-fullstack-langgraph-quickstart.git
cd gemini-fullstack-langgraph-quickstart
```

#### 2. 设置 API 密钥
```bash
# 进入后端目录
cd backend

# 复制环境变量模板
cp .env.example .env

# 编辑 .env 文件，添加你的 Gemini API 密钥
echo 'GEMINI_API_KEY="your_actual_api_key_here"' > .env
```

#### 3. 安装依赖
```bash
# 后端依赖
cd backend
pip install .

# 前端依赖
cd ../frontend
npm install
```

### 第二步：运行项目

#### 方法一：使用 Makefile (推荐)
```bash
# 在项目根目录
make dev
```

#### 方法二：分别启动
```bash
# 终端1 - 启动后端
cd backend
langgraph dev

# 终端2 - 启动前端
cd frontend
npm run dev
```

### 第三步：测试功能
- 打开浏览器访问 `http://localhost:5173/app`
- 尝试问一个研究性问题，如："What are the latest developments in quantum computing?"
- 观察 Agent 的工作过程

## 🔬 实践练习

### 练习 1：理解工作流程 (30分钟)

#### 目标
观察和理解 Agent 的完整工作流程

#### 步骤
1. 启动应用并打开 LangGraph UI (`http://127.0.0.1:2024`)
2. 在前端界面提问："最近人工智能领域有什么重大突破？"
3. 在 LangGraph UI 中观察执行轨迹
4. 记录每个节点的输入输出

#### 观察要点
- [ ] 生成了哪些搜索查询？
- [ ] 搜索结果的质量如何？
- [ ] Agent 进行了几轮迭代？
- [ ] 最终答案的引用来源是否准确？

### 练习 2：修改提示词 (45分钟)

#### 目标
通过修改提示词来改变 Agent 行为

#### 步骤
1. 打开 `backend/src/agent/prompts.py`
2. 找到 `QUERY_GENERATION_PROMPT`
3. 修改提示词，让 Agent 生成更多元化的查询
4. 重启后端服务测试效果

#### 实验方向
```python
# 原始提示词样例修改
QUERY_GENERATION_PROMPT = """
你是一个专业的搜索查询生成专家。
基于用户的问题，生成5-7个不同角度的搜索查询。

要求：
1. 涵盖问题的核心概念
2. 包含相关的学术术语
3. 考虑时间因素（最新、近期、趋势）
4. 包含不同的视角（技术、商业、社会影响）

用户问题: {question}

请生成搜索查询列表：
"""
```

### 练习 3：添加新的搜索工具 (60分钟)

#### 目标
集成额外的搜索源，如学术论文搜索

#### 步骤
1. 在 `backend/src/agent/tools_and_schemas.py` 中添加新工具
2. 修改 `graph.py` 中的搜索节点
3. 更新状态定义以支持多源搜索

#### 实现示例
```python
# 在 tools_and_schemas.py 中添加
def search_academic_papers(query: str) -> List[dict]:
    """搜索学术论文的模拟实现"""
    # 这里可以集成 arXiv API 或其他学术搜索服务
    return [
        {
            "title": f"Academic paper about {query}",
            "url": "https://arxiv.org/example",
            "snippet": f"This paper discusses {query}...",
            "source": "arXiv"
        }
    ]
```

### 练习 4：前端界面定制 (45分钟)

#### 目标
优化用户界面，添加更好的可视化

#### 步骤
1. 打开 `frontend/src/App.tsx`
2. 添加搜索进度显示
3. 改进引用来源的展示方式
4. 添加对话历史功能

#### 改进方向
- 显示搜索轮数和状态
- 美化引用链接的展示
- 添加复制答案功能
- 实现暗色主题切换

## 🐛 常见问题解决

### 问题1：API 密钥错误
```
错误：Authentication failed
解决：检查 .env 文件中的 GEMINI_API_KEY 是否正确
```

### 问题2：端口冲突
```
错误：Port 2024 is already in use
解决：关闭其他占用端口的程序，或修改配置文件中的端口
```

### 问题3：依赖安装失败
```
错误：Package installation failed
解决：
- Python：确保使用 Python 3.8+
- Node.js：确保使用 Node.js 18+
- 考虑使用虚拟环境：python -m venv venv
```

### 问题4：搜索功能不工作
```
错误：Search results empty
解决：
- 检查网络连接
- 验证 Google Search API 配置
- 查看后端日志获取详细错误信息
```

## 📊 性能测试

### 测试脚本
创建一个简单的性能测试：

```python
# test_performance.py
import time
import asyncio
from agent.app import graph

async def test_question(question: str):
    start_time = time.time()
    
    result = await graph.ainvoke({
        "messages": [{"role": "user", "content": question}]
    })
    
    end_time = time.time()
    return {
        "question": question,
        "duration": end_time - start_time,
        "iterations": result.get("reflection_count", 0),
        "answer_length": len(result.get("final_answer", ""))
    }

# 测试不同复杂度的问题
test_questions = [
    "What is Python?",  # 简单
    "Latest trends in machine learning",  # 中等
    "Comprehensive analysis of quantum computing impact on cryptography"  # 复杂
]
```

## 🎯 学习检查点

### 基础理解 ✅
- [ ] 成功运行原始项目
- [ ] 理解 Agent 的工作流程
- [ ] 能够解释每个节点的作用

### 代码修改 ✅
- [ ] 成功修改提示词并看到效果
- [ ] 理解状态在节点间的传递
- [ ] 能够添加简单的日志输出

### 功能扩展 ✅
- [ ] 尝试集成新的工具或API
- [ ] 修改前端界面并改善用户体验
- [ ] 理解前后端的通信机制

### 部署运维 ✅
- [ ] 使用 Docker 成功部署
- [ ] 理解配置文件的作用
- [ ] 能够排查常见问题

## 🔗 实用链接

- [原始项目仓库](https://github.com/google-gemini/gemini-fullstack-langgraph-quickstart)
- [LangGraph 官方文档](https://langchain-ai.github.io/langgraph/)
- [Google Gemini API](https://ai.google.dev/)
- [React 文档](https://react.dev/)
- [FastAPI 文档](https://fastapi.tiangolo.com/)

---

**记住：边做边学，遇到问题就是学习的好机会！** 🎉
