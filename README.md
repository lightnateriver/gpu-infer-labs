# gpu-infer-labs

GPU推理优化实验、可移植代码、匿名证据与报告。

## 当前更新

[Qwen3-Omni Thinking · RTX5090 · N3/K3＋多FULL Graph＋KV6.5GiB](models/qwen3-omni-thinker-thinking/5090/native-ngram3-multifull-kv6p5-tp1-c4/readme.md)：TP1/C4，Thinking计入，三轮45/45完整、零抢占，**3.575有效条/分钟**，完整轮输出TPS/卡中位数**310.22**。相对本轮同条件C4基线3.240条/分钟提升10.33%；不是相对历史不同协议的直接增益。

| 模型/硬件 | 最新方案 | 历史方案 |
|---|---|---|
| [Qwen3-Omni / RTX5090](models/qwen3-omni-thinker-thinking/5090/readme.md) | [多FULL＋KV优化](models/qwen3-omni-thinker-thinking/5090/native-ngram3-multifull-kv6p5-tp1-c4/readme.md) | [原生N3](models/qwen3-omni-thinker-thinking/5090/native-ngram3-async-fp8-tp1-c4/readme.md)、[Omni FP8](models/qwen3-omni-thinker-thinking/5090/async-fp8-gemm-fp8-kv-tp1-c4/readme.md) |

每项保留配置、runtime、启动/测试方式、环境、输入合同、匿名证据和独立HTML。有效吞吐、完整轮TPS与精度分别报告；历史输出长度/协议可能不同，不能把跨报告比例当作单项消融或稳定收益。需要自备模型和有权使用的冻结输入；不发布私有业务内容与访问凭证。
