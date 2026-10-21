# 模型推理实验

- [Qwen3-Omni Thinker / Thinking](qwen3-omni-thinker-thinking/readme.md)
- [RTX5090 当前方案：多 FULL Graph＋KV6.5GiB](qwen3-omni-thinker-thinking/5090/native-ngram3-multifull-kv6p5-tp1-c4/readme.md)：TP1/C4、Thinking计入，3.575有效条/分钟，完整轮310.22TPS/卡中位数；三轮45/45完整、零抢占，相对本轮C4基线+10.33%。
- [历史原生N3](qwen3-omni-thinker-thinking/5090/native-ngram3-async-fp8-tp1-c4/readme.md)与[Omni FP8](qwen3-omni-thinker-thinking/5090/async-fp8-gemm-fp8-kv-tp1-c4/readme.md)继续保留。跨报告协议、输出长度和统计方式不同，不直接归因单项收益；完整性不是人工Caption精度。
