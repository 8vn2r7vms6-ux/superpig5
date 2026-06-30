# Ollama分布式推理集群

## 路由策略（2026-06-30验证通过）

| 任务类型 | 路由目标 | 模型 | 预期响应 |
|---------|---------|------|---------|
| 日常对话 | Mac ⑤ | qwen2.5:7b | <3s |
| 复杂推理 | Mac ⑨ | glm4:9b | <5s |
| 代码生成 | Mac ⑥ | qwen2.5-coder:14b | <10s |
| 大规模推理 | Mac ⑤ | qwen2.5:14b | <15s |
| 中文写作 | Mac ⑨ | glm4:9b | <5s |
| 向量嵌入 | Mac ⑦ | nomic-embed-text | <1s |
| 量化分析 | Hermes | deepseek-r1:7b | <8s |
| 深度推理 | Mac ⑧(待) | deepseek-r1:14b | <12s |

## 使用方法

```bash
# 通过ollama_router.py
python3 ~/.qclaw/workspace/bin/ollama_router.py general "你的问题"

# 或直接调用指定机器
curl -X POST http://192.168.1.2:11434/api/generate \
  -d '{"model":"qwen2.5:7b","prompt":"问题","stream":false}'
```

## 实测结果（2026-06-30）

- Mac ⑥ 双14B并发: 两模型都能完成，响应时间10-12s（串行）
- Mac ⑤ qwen2.5:14b: 7.9s
- Mac ⑨ glm4:9b: 4.8s
- Hermes deepseek-r1:7b: 4.8s
