<div align="center">

<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=600&size=28&duration=3000&pause=1000&color=6C8EEB&center=true&vCenter=true&width=600&lines=Java+Backend+Developer;AI+Application+Builder;AI+Agent+Developer" alt="Typing SVG" />

<img src="https://komarev.com/ghpvc/?username=1byteone&style=for-the-badge&color=blue" alt="Profile views" />

<br/>

### Hi there 👋 I'm 1byteone

> Building intelligent systems, one line of Java at a time.

</div>

---

### 👨‍💻 About Me

从 Java 企业后端开发起步，深耕 Spring Boot 微服务架构多年。随着大模型时代的到来，将技术重心逐步转向 AI 应用与 Agent 开发，致力于将 LLM 能力落地到真实业务场景。

目前专注于企业级 AI Agent 框架搭建、多智能体协同调度以及 RAG 知识库应用。相信 AI Agent 将重塑企业软件的交互范式——从"点击操作"到"自然对话"，从"固定流程"到"自主决策"。

- 🏗️ 构建了 **ruoyi-ai** — 一站式企业 AI 应用开发框架
- 🤖 开发了 **mewpaw-code** — Java 21 CLI Coding Agent
- ✍️ 实践了 **ai-passage-creator-demo** — 多 Agent 协作内容生成系统

---

### 🛠️ Tech Stack

#### Backend

![Java](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring_Boot-6DB33F?style=for-the-badge&logo=spring-boot&logoColor=white)
![MyBatis](https://img.shields.io/badge/MyBatis-000000?style=for-the-badge&logo=mybatis&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-DC382D?style=for-the-badge&logo=redis&logoColor=white)
![Maven](https://img.shields.io/badge/Maven-C71A36?style=for-the-badge&logo=apache-maven&logoColor=white)

#### AI & Agent

![OpenAI](https://img.shields.io/badge/OpenAI-412991?style=for-the-badge&logo=openai&logoColor=white)
![LangChain](https://img.shields.io/badge/LangChain-1C3C3C?style=for-the-badge&logo=langchain&logoColor=white)
![Spring AI](https://img.shields.io/badge/Spring_AI-6DB33F?style=for-the-badge&logo=spring&logoColor=white)
![AI Agent](https://img.shields.io/badge/AI_Agent-7B42BC?style=for-the-badge&logo=robot-framework&logoColor=white)
![LLM](https://img.shields.io/badge/LLM-FF6F00?style=for-the-badge&logo=openai&logoColor=white)

#### Tools

![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Git](https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)
![IntelliJ IDEA](https://img.shields.io/badge/IntelliJ_IDEA-000000?style=for-the-badge&logo=intellij-idea&logoColor=white)

---

### 📊 GitHub Stats

<div align="center">

<img height="180em" src="https://github-readme-stats.vercel.app/api?username=1byteone&show_icons=true&theme=tokyonight&include_all_commits=true&count_private=true" />
<img height="180em" src="https://github-readme-stats.vercel.app/api/top-langs/?username=1byteone&layout=compact&theme=tokyonight" />

<br/>

<img src="https://streak-stats.demolab.com/?user=1byteone&theme=tokyonight" alt="GitHub Streak" />

</div>

---

### 🚀 Featured Projects

#### 🏗️ ruoyi-ai — 企业级 AI 应用开发框架

> 一站式 AI 应用开发平台，支持多厂商大模型统一接入、企业知识库 RAG、可视化流程编排与多智能体协同调度。

`Java` `Spring Boot 3.5` `LangChain4j` `Python` `MySQL` `Redis` `Docker`

- 🔗 **多模型统一接入** — 兼容 OpenAI / DeepSeek / 通义千问 / MiniMax，一行配置切换
- 🧠 **企业知识库 RAG** — 本地 RAG + 向量库（Milvus/Weaviate），高精度检索增强
- 🔄 **可视化流程编排** — 拖拽式 AI 工作流设计，Supervisor 多智能体协同
- 🛡️ **企业级安全** — Sa-Token + JWT 双认证，数据脱敏，全链路审计

<div align="center">

[![ruoyi-ai](https://github-readme-stats.vercel.app/api/pin/?username=1byteone&repo=ruoyi-ai&theme=tokyonight)](https://github.com/1byteone/ruoyi-ai)

</div>

<details>
<summary>📐 架构图</summary>

```mermaid
graph TB
    subgraph "Frontend"
        A[Vue 3 用户端] --- B[Vben Admin 管理端]
    end
    subgraph "Gateway"
        C[API Gateway]
    end
    subgraph "Core Modules"
        D[ruoyi-chat<br/>RAG 知识库] --- E[ruoyi-aiflow<br/>流程编排]
        F[ruoyi-workflow<br/>工作流] --- G[ruoyi-system<br/>系统管理]
    end
    subgraph "AI Engine"
        H[LangChain4j Agent] --> I[Supervisor 调度]
        I --> J[Model Router]
    end
    subgraph "Models"
        K[OpenAI] -.- L[DeepSeek] -.- M[通义千问] -.- N[MiniMax]
    end
    A --> C --> D & E & F & G
    D --> H
    J --> K & L & M & N
```

</details>

---

#### ✍️ ai-passage-creator-demo — AI 爆款文章生成器

> 基于多 Agent 协作的智能内容创作系统，覆盖选题分析、文案生成、智能配图到在线支付的完整链路。

`Java` `Spring Boot 3.5` `Spring AI` `Go` `Python` `Vue 3` `Stripe`

- 🤝 **多 Agent 编排** — 选题 Agent + 文案 Agent + 配图 Agent 协同创作，流水线式内容生产
- 🎨 **智能配图选择** — 多种配图方式（AI 生图 / 素材库 / 混搭），自动匹配最佳方案
- 💳 **Stripe 在线支付** — 完整商业化闭环，支持付费内容生成
- 🧩 **三语言后端** — 同时提供 Java / Go / Python 三种版本，技术选型灵活

<div align="center">

[![ai-passage-creator-demo](https://github-readme-stats.vercel.app/api/pin/?username=1byteone&repo=ai-passage-creator-demo&theme=tokyonight)](https://github.com/1byteone/ai-passage-creator-demo)

</div>

<details>
<summary>📐 多 Agent 协作流程</summary>

```mermaid
graph LR
    U[👤 用户需求] --> O[🎯 Supervisor 调度]
    O --> A1[📋 选题 Agent]
    O --> A2[✍️ 文案 Agent]
    O --> A3[🎨 配图 Agent]
    O --> A4[🔍 审核 Agent]
    A1 & A2 & A4 -.-> LLM[🧠 LLM API]
    A3 -.-> IMG[🖼️ Image API]
    O --> PAY[💳 Stripe]
    O --> PUB[📤 发布]
```

</details>

---

#### 🤖 mewpaw-code — Java 21 CLI Coding Agent

> 纯 Java 实现的命令行编码智能体，ReAct Agent Loop + 5 层安全沙箱 + 6 个内置工具，TUI/REPL 交互体验。

`Java 21` `ReAct Agent` `CLI/TUI` `Docker` `Python`

- 🌀 **ReAct Agent Loop** — Think → Act → Observe 循环，自主规划和执行编码任务
- 🔒 **5 层安全沙箱** — 命令白名单 + 文件隔离 + 网络限制 + 资源配额 + 审计日志
- 🛠️ **6 个内置工具** — 文件读写、命令执行、代码搜索、Git 操作、依赖管理、测试运行
- 🖥️ **TUI/REPL 交互** — 终端原生体验，支持对话式编程和实时反馈

<div align="center">

[![mewpaw-code](https://github-readme-stats.vercel.app/api/pin/?username=1byteone&repo=mewpaw-code&theme=tokyonight)](https://github.com/1byteone/mewpaw-code)

</div>

<details>
<summary>📐 ReAct Agent Loop</summary>

```mermaid
graph LR
    U[👤 自然语言任务] --> T[💭 Think 分析规划]
    T --> A[⚡ Act 执行工具]
    A --> T1[📁 File I/O]
    A --> T2[💻 Command]
    A --> T3[🔍 Search]
    A --> T4[📦 Git]
    A --> T5[📚 Deps]
    A --> T6[🧪 Test]
    T1 & T2 & T3 & T4 & T5 & T6 --> O[👁️ Observe]
    O -->|未完成| T
    O -->|完成| R[✅ Response]
```

</details>

---

### 🎯 Currently Focus

- 🔭 I'm currently working on **Java + AI Agent application development**
- 🌱 I'm currently learning **AI Agent frameworks, LLM application architecture**
- 👯 I'm looking to collaborate on **AI open-source projects**

---

### 📬 Get in Touch

<div align="center">

[![Email](https://img.shields.io/badge/Email-yjs_0831%40qq.com-blue?style=for-the-badge&logo=gmail&logoColor=white)](mailto:yjs_0831@qq.com)

<br/>

*"Building intelligent systems, one line of Java at a time."*

</div>