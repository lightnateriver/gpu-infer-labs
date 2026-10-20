# gpu-infer-labs
GPU 推理优化散装合集

## 模型方案

- [Qwen3-Omni Thinking · RTX 5090](models/qwen3-omni-thinker-thinking/5090/readme.md)：TP1/C4，异步调度 + FP8 GEMM + FP8 KV；记录吞吐 3.024 条/分钟。
