# RTX 5090 · Qwen3-Omni Thinker / Thinking

| 方案 | 运行时 | 配置 | 完整任务吞吐 | 输出 token/s/卡 |
|---|---|---|---:|---:|
| [原异步 FP8 GEMM + FP8 KV](async-fp8-gemm-fp8-kv-tp1-c4/readme.md) | vLLM-Omni | TP1 / C4 | 3.024 条/分钟 | 238.54 |
| [新增原生 N3/K3 + Async + FP8](native-ngram3-async-fp8-tp1-c4/readme.md) | native vLLM | TP1 / C4 | **3.161 条/分钟** | **273.71** |

数值分别来自各自两轮实测，包含 Thinking；每条件 15 个不同视频 × 2 轮。不同运行时结果只作背景，不能据此归因 n-gram 收益。原 Omni 方案同配置另一次复测为 2.815 条/分钟，显示运行波动。

新增报告包含更合适的原生无 n-gram 对照：3.090 条/分钟、247.21 token/s/卡。N3 为 3.161 / 273.71，TPOT 从 13.26 降至 11.48 ms；任务吞吐 +2.27%，但输出变长，尚未证明稳定收益。N5 为 3.188 / 277.17，TPOT 12.32 ms；未保留。不要仅按 token TPS 宣称任务处理能力或 Caption 质量提高。

两套方案都用非官方 Thinking-heretic NVFP4 权重；96 个 attention 线性层 FP8，MoE NVFP4，48 层 FP8 KV；不是 BF16 Thinking 全模型。每个目录独立提供版本、配置、核心代码、实践测试方案、匿名证据与报告。新方案禁用 Omni 插件，修复原生多模态 modality metadata，并使用 GPU n-gram proposer。

需要自备有权限使用的同指纹模型和冻结输入；仓库不分发权重、媒体、业务 prompt、原始 Caption、原数据来源、主机信息或凭证。各 README 已补充新方案入口。
