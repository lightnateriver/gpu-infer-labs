# 模型推理实验

- [Qwen3-Omni Thinker / Thinking](qwen3-omni-thinker-thinking/readme.md)

## 新增原生 n-gram 方案

[原生 vLLM N3/K3 · TP1/C4](qwen3-omni-thinker-thinking/5090/native-ngram3-async-fp8-tp1-c4/readme.md)：2026-10-21 两轮观测 **3.161 条/分钟、273.71 token/s/卡**，Thinking 计入；与原生无 n-gram 的对照及 N5 试验见新报告。该数值不是上文 Omni 配置的复测，也未证明稳定吞吐或语义精度优势。
