# Agent-RAG-System

## 项目简介

本项目是一个基于RAG与Agent架构的智能问答系统。

系统结合：

- 大语言模型
- 向量数据库
- 工具调用机制
- 动态Prompt
- 上下文管理

实现了一个具备“检索+推理+调用工具”能力的智能体系统。

支持：

* 本地文档语义检索
* 多工具调用（天气 / 用户信息 / 外部数据）
* 动态 Prompt 切换（普通问答 / 报告生成）
* 流式对话（Streamlit UI）

---

## 项目结构

```bash
agent/
│
├── agent/                      #Agent模块
│   ├── react_agent.py
│   └── tools/
│       ├── agent_tools.py
│       └── middleware.py
│
├── model/                      #模型管理
│   └── factory.py
│
├── rag/                        #RAG模块
│   └── rag_service.py
│
├── utils/                      #工具模块
│   ├── config_handler.py
│   ├── file_handler.py
│   ├── logger_handler.py
│   ├── path_tool.py
│   └── prompt_loader.py
│
├── config/                     #配置文件
│   ├── rag.yml
│   ├── chroma.yml
│   ├── prompts.yml
│   └── agent.yml
│
├── logs/                       #日志
│
├── app.py                      #Streamlit入口
└── requirements.txt
核心模块说明
1. Agent系统（agent/）

基于 LangChain + LangGraph 实现：

工具调用（Tool Calling）
中间件机制（Middleware）
动态 Prompt 切换
2. 工具系统（agent/tools/agent_tools.py）

内置工具：

RAG检索工具
天气查询
用户信息获取
外部业务数据查询
报告上下文注入

特点：

标准化 Tool 封装
易扩展
3. 中间件机制（middleware.py）

功能：

工具调用监控
日志记录
动态上下文注入
Prompt切换控制
4. 模型工厂（model/factory.py）

实现：

聊天模型（ChatTongyi）
Embedding模型（DashScopeEmbeddings）

特点：

工厂模式
配置驱动切换
5. RAG模块（rag/）

实现：

文档加载（PDF / TXT）
文本切分
向量存储（Chroma）
语义检索
6. Prompt管理（prompt_loader.py）

支持：

系统 Prompt
RAG Prompt
报告 Prompt

特点：

配置解耦
动态加载
7. 文件处理（file_handler.py）

功能：

MD5 去重
多层目录扫描
文档加载
8. 日志系统（logger_handler.py）

支持：

控制台日志
文件日志
自动日志文件生成
9. Streamlit UI（app.py）

功能：

聊天界面
流式输出
会话管理（session_state）
环境依赖

建议 Python 3.10+

安装依赖：

pip install -r requirements.txt

核心依赖：

langchain
langchain-community
langchain-text-splitters
langchain-chroma
chromadb
streamlit
PyYAML
使用方法
启动系统
streamlit run app.py
示例功能

用户输入：

帮我生成一份用户使用报告

系统流程：

调用工具获取用户ID
获取月份
查询外部数据
动态切换 Report Prompt
生成报告
