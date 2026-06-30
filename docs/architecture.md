# 三Agent架构

## 节点（2026-06-30更新）

| 节点 | Agent | IP (局域网) | 用户 | 角色 |
|------|-------|------------|------|------|
| 🦞 QClaw | OpenClaw | 192.168.1.10 | maliang | **协调中枢** - 任务编排、消息路由、腾讯生态、定时任务 |
| 🐴 Hermes | Hermes | 192.168.1.4 | xuanjing8 | **执行中枢** - 代码开发、量化回测、GitHub操作、deepseek-r1:7b |
| 👤 OpenHuman | OpenHuman | 192.168.1.8 | xuanjing3 | **记忆中枢** - 657 RPC方法、长期记忆、用户画像、Model Council |
| 🗄️ NAS | 极空间 | 192.168.1.7:10000 | 13567550450 | **存储中枢** - 930GB NVMe、定时任务、策略运行 |

## 助手Mac集群（Ollama分布式推理）

| Mac | IP | 用户 | 模型 | 用途 |
|-----|-----|------|------|------|
| Mac ⑤ | 192.168.1.2 | xuanjing5 | qwen2.5:7b + qwen2.5:14b | 通用主力 |
| Mac ⑥ | 192.168.1.5 | xuanjing2 | qwen2.5:14b + qwen2.5-coder:14b | 代码专家 |
| Mac ⑦ | 192.168.1.6 | xuanjing6 | nomic-embed-text + qwen2.5:7b | 嵌入+快速 |
| Mac ⑧ | 192.168.1.9 | xuanjing4 | deepseek-r1:14b (macOS升级后安装) | 深度推理 |
| Mac ⑨ | 192.168.1.13 | xuanjing7 | glm4:9b | 国产/中文 |
| Windows | 192.168.1.15 | superpig5 | RTX3060 | 视频渲染 |

## 协作场景

1. **量化报告闭环**: QClaw设计需求 → Hermes执行回测 → OpenHuman存储记忆 → NAS运行策略
2. **分布式推理**: QClaw路由任务 → Ollama集群推理 → 结果返回
3. **记忆同步**: 三节点通过OpenHuman RPC同步
4. **视频制作**: QClaw生成脚本 → Windows RTX3060渲染

## 工具路径

- Ollama路由: `/Users/maliang/.qclaw/workspace/bin/ollama_router.py`
- 集群监测: `/Users/maliang/.qclaw/workspace/bin/cluster_monitor.py`
- 协作状态: `/Users/maliang/.qclaw/workspace/bin/collab-state.sh`
- 用户画像: OpenHuman `~/.openhuman/users/*/workspace/PROFILE.md`
