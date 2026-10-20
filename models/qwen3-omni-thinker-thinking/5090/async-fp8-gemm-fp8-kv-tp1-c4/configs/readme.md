# 配置

- `deploy.json`：3.024 条/分钟历史方案的原部署 JSON。TP1/C4、异步调度、96 层 FP8 GEMM、FP8 KV 6.25 GiB、上下文 65536、chunked prefill 4096、Graph `[1,2,4]`。
- `kv-scales.json`：原 48 层 K/V 静态 scales。metadata 记录 320 个校准样本、`heldout_used=false`、max-abs/448 和 10% 余量；不含校准数据。不能无验证地迁移到不同权重。
- `model-fingerprint.json`：实测权重及 tokenizer/processor 等 10 个文件的 SHA256；无本地路径或模型文件。

启动脚本复制部署 JSON 到本地状态目录，设置 `KV_SCALES_FILE` 后启动。`devices: "0"` 是 CUDA_VISIBLE_DEVICES 映射后的逻辑卡 0；物理卡由 `start.sh --gpu N` 指定。

配置 JSON 未改写成 BF16 KV。完整启动、版本、测试方式和指标见 [方案说明](../readme.md)。
