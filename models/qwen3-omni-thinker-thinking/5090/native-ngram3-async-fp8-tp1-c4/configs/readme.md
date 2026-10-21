# 配置与权重指纹

- `deploy.json`：默认 N3/K3，method=ngram_gpu，num_speculative_tokens=3，prompt_lookup_min=max=3。
- `control.json`：原生无 n-gram，capture sizes=[1,2,4]，其余主要精度/调度条件一致。
- `ngram5.json`：后续 N5/K5 对照，capture=[1,2,4,6,12,24]、max=24，历史未选用。不得把它的 3.188 条/分钟标作 N3 结果。
- `kv-scales.json`：原冻结 K/V scales 的数值，heldout_used=false；worker 自动去掉旧命名空间 thinker. 前缀，匹配原生层名。
- `model-fingerprint.json`：原模型 10 个文件 SHA256；启动时重新校验。不是 N3 实验重新全量校验的证明。

JSON 的模型目录/alias/端口为通用值，启动包装脚本覆盖模型目录与端口。其余计算参数来自实测配置。N3 capture=[1,2,4,8,16]，实际审计 V1 GPUModelRunner / NgramProposerGPU / async=true；6.25 GiB FP8 KV、XQA、BF16 Q、96 attention FP8 线性层、TP1/C4。

参数及统计边界见 [方案说明](../readme.md)。
