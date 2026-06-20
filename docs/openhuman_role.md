# 🧠 OpenHuman 角色定义：个人记忆与知识中枢

## 核心理念

> 让整个智能体集群越来越懂你，记录你的每一条偏好、每一个习惯、每一次决策→ OpenHuman 就是集群的"大脑记忆半球"

## 定位：集群记忆中枢（Memory Hub）

**不是另一个对话 AI，而是集群的永久知识层。**

| 节点 | 角色 | 类比 |
|------|------|------|
| 🦞 **QClaw**（本机） | **协调者 Orchestrator** | 消息路由、任务分配、决策者 |
| 🐴 **Hermes**（Mac②） | **执行者 Executor** | 代码开发、终端命令、模型推理 |
| 👤 **OpenHuman**（Mac③） | **记忆中枢 Memory Hub** | 长期记忆、用户画像、知识图谱 |

## OpenHuman 的 7 大独特能力

### 1️⃣ Memory Tree（最强记忆系统）
- **树状分层结构**：瞬时→短期→长期，自动分级
- **时序索引**：可追溯完整任务链路
- **TokenJuice 压缩**：3.7x 压缩比，同空间存更多
- **语义搜索**：精准回忆过去任何对话或决策

### 2️⃣ Learning Facets（用户画像）
- 自动学习用户偏好、习惯、工作模式
- 可保存 profile，跨 session 持久化
- LinkedIn 数据增强

### 3️⃣ Memory Sources（外部数据同步）
- 可同步 Gmail → 自动学习邮件习惯
- 可同步 Slack → 学习团队沟通模式
- 可同步 GitHub → 学习代码偏好
- 可同步 Notion → 学习知识管理习惯
- 可同步 WhatsApp → 社交模式

### 4️⃣ Composio（200+ 外部工具）
- **比 QClaw 和 Hermes 的代理更广泛的连接能力**
- 接入 ClickUp、Linear 等项目管理
- 接入 Gmail 收发邮件
- 接入 Notion/Slack 等协作工具

### 5️⃣ Screen Intelligence（屏幕理解）
- 可以截图 + 理解屏幕内容
- 可以模拟鼠标键盘操作
- **意味着：可以观察用户如何使用电脑，学习工作流程**

### 6️⃣ Voice Pipeline（语音全链路）
- TTS 语音合成
- STT 语音识别（Whisper）
- 语音克隆（Piper）

### 7️⃣ Cryptocurrency（Web3 钱包）
- 资产管理、交易执行
- Web3 DApp 交互

## 具体工作流

### 知识收集 → 分析 → 记忆

```
用户对话/操作
    │
    ▼
QClaw 识别到"这值得记住"
    │  (将关键信息发送给 OpenHuman)
    ▼
OpenHuman 调用 memory_tree_ingest() 
    │  或 learning_save_profile()
    ▼
Memory Tree 存储 → 更新用户画像
```

### 回忆 / 查询

```
QClaw 启动时 / 需要上下文
    │
    ▼
调用 OpenHuman API 查询用户画像
    │  (query memory_tree or learning facets)
    ▼
获取用户的完整偏好历史
    │
    ▼
QClaw 据此调整对话风格和决策
```

### 持续学习（后台）

```
OpenHuman 后台 24 小时运行
    │
    ├── 每 20 分钟 sync memory sources（Gmail/Slack/GitHub）
    ├── 自动更新 Learning Facets
    ├── 维护 Memory Tree 树形索引
    └── 定期生成"用户画像快照"
```

## 对"越来越懂你"的贡献

| 时间维度 | QClaw 能做到 | Hermes 能做到 | OpenHuman 能贡献 |
|----------|-------------|--------------|-----------------|
| 单次对话 | ✅ 全量记忆 | ✅ 全量记忆 | 可持久化到永久存储 |
| 当日 | ✅ 工作记忆 | ✅ 工作记忆 | 树状索引分类存储 |
| 本周 | ⚠️ 可能遗忘 | ⚠️ 可能遗忘 | ✅ 完整时间线可追溯 |
| 当月 | ❌ 遗忘 | ❌ 遗忘 | ✅ 可精准回忆 |
| 用户画像 | ❌ 无 | ❌ 无 | ✅ Learning Facets |
| 习惯学习 | ❌ 无 | ❌ 无 | ✅ 自动构建 profile |
| 多数据源融合 | ❌ 单一 | ❌ 单一 | ✅ Gmail+GitHub+Slack |

## 技术实现

OpenHuman 暴露 JSON-RPC API（端口 7788），QClaw 通过 SSH 调用其接口：

### 核心 API 调用

```python
# 1. 存储知识
rpc_call("openhuman.memory_tree_ingest", {
    "content": "用户喜欢简洁的回复风格，不喜欢废话",
    "source": "qclaw_observation",
    "importance": "high"
})

# 2. 更新用户画像
rpc_call("openhuman.learning_save_profile", {
    "facet": "communication_preference",
    "value": "prefers_concise_chinese",
    "source": "qclaw_analysis"
})

# 3. 查询记忆
rpc_call("openhuman.memory_tree_recall", {
    "query": "用户对量化交易的有什么偏好?",
    "top_k": 5
})

# 4. 获取完整画像
rpc_call("openhuman.learning_get_facet", {
    "name": "user_profile"
})
```

### 连接 Compositio（未来）

```bash
# 通过 OpenHuman 连接 Gmail - 自动学习邮件习惯
rpc_call("openhuman.composio_authorize", { "toolkit": "gmail" })

# 之后 OpenHuman 可以自动同步和分析邮件
rpc_call("openhuman.memory_sources_add", {
    "toolkit": "gmail",
    "label": "my_emails"
})
```

## 需要你操作的开通项

以下功能需要你**授权登录**后才能生效：

1. **Gmail 连接** → 学习邮件沟通习惯
2. **GitHub 连接** → 学习代码风格偏好
3. **Slack/Notion 连接** → 学习工作流
4. **Voice 设置** → 语音能力

这些通过 OpenHuman 的 Composio OAuth 流程完成（在 OpenHuman app 内操作）。
