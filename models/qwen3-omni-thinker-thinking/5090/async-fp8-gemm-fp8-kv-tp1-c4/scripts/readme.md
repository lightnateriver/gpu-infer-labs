# 启动与测试脚本

适用 RTX 5090 32 GiB 单卡，TP1/C4；vLLM/vLLM-Omni 0.30.0；Python 3.10。先按 [方案说明](../readme.md) 准备等价环境和私有数据。

```bash
bash scripts/start.sh --gpu 0 --model-dir "$MODEL_DIR" --port 48121
bash scripts/benchmark.sh --data-dir "$DATA_DIR" --prepared-dir "$PREPARED_DIR"   --run-dir .local/my-caption-run --concurrency 4 --rounds 2
python3 scripts/summarize.py --run-dir .local/my-caption-run --rounds 2
python3 scripts/stop.py
```

两次测试各完整预热 1 条，再测冻结的 15 条；Thinking 计入。历史合并结果 3.023557 条/分钟、238.535153 token/s/卡。温度 0 不保证动态组批下逐 token 复现。

- `check_environment.py` 检查保存的版本记录和工具可用性，不创建 CUDA context。
- `start.py` 参数化私有路径、核对选卡空闲/端口和模型指纹；设置原 JIT、Graph、FP8 KV/线性层审计环境，启动独立本地进程 session。只监听 localhost。
- `api_compat.py` 是原 Python 3.10 协议 dataclass 导入兼容修复。
- `benchmark.py` 调用保留的流式客户端，先 token 预检再预热/正式测试；不启动或停止其他服务。
- `summarize.py` 按总量/总 wall 汇总，检查 Thinking、完整性和 API 计数，不把错误/截断列为完整输出。
- `ops.py` / `stop.py` 依据 UID、PID 启动时间和 session 验证，只停止 receipt 对应的作业。

receipt/日志/缓存/原始输出默认保存在忽略的 `.local/`。VLLM_API_KEY 只从环境读取，不写入公开配置。新包装脚本为整理后的可移植入口，没有额外运行 GPU 测试；核心实测代码和匿名结果见 benchmark/runtime/evidence。
