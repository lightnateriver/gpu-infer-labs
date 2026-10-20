# 原实测 runtime workers

卡型：RTX 5090，SM120；vLLM / vLLM-Omni 0.30.0。启动由 [scripts/start.py](../scripts/start.py) 注入本目录 PYTHONPATH，无需安装成全局模块。

- `caption_worker.py`：保留实测中的图像+视频+原音轨 DeepStack 位置掩码修复，并移除该权重压缩配置中过宽的 ignore 规则，断言 48 层专家实际使用 NVFP4。
- `kv_audit_worker.py`：核对物理 GPU、48 层 KV 的实际 dtype/分配视图，加载原 K/V scales，记录实际 FlashInfer/XQA 路由；独立模块包含原校准支持，默认启动不启用校准。
- `mixed_fp8_worker.py`：断言 48 QKV + 48 O 为 FP8、实际 CutlassFP8ScaledMMLinearKernel；router/head 保持 BF16；记录实际 OmniARAsyncScheduler。

三份核心源码按原内容保留。它们针对上述精确包版本和 checkpoint 结构；升级后若断言不匹配应先定位实现差异。原权重不会写回磁盘。

这些文件是兼容与审计实现，不是质量验收证明。性能测试、启动命令与已测指标见 [方案说明](../readme.md)。
