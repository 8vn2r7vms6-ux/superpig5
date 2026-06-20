# 三Agent架构

## 节点

| 节点 | Agent | 设备 | IP (局域网) | 用户 | 角色 |
|------|-------|------|------------|------|------|
| 🦞 QClaw | OpenClaw | Mac ① | 192.168.1.3 | maliang | **主控 Agent** - 任务编排、消息路由、知识库(ima)、定时任务 |
| 🐴 Hermes | Hermes | Mac ② | 192.168.1.4 | xuanjing8 | **开发 Agent** - 代码开发、模型推理、终端执行、GitHub操作 |
| 👤 OpenHuman | OpenHuman | Mac ③ | 192.168.1.5 | xuanjing2 | **数据桥接 Agent** - RPC接口、事件订阅、技能注册、Ollama推理 |

## 协作场景

1. **代码开发闭环**: QClaw设计需求 → Hermes写代码 → Push到GitHub → (待定)
2. **推理分发**: QClaw分发复杂推理任务给Hermes/OpenHuman
3. **记忆同步**: 三节点通过GitHub同步MEMORY.md
4. **负载均衡**: 资源密集型任务分配给最合适的节点
