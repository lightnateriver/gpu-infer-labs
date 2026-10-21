# 运行脚本

| 文件 | 用途 |
|---|---|
| start.sh / start.py | Linux 参数化启动；默认 --variant ngram3；可选 control/ngram5；校验模型/工具链/卡空闲与实际 runtime 审计 |
| benchmark.sh / benchmark.py | 冻结 manifest 预检；每轮最大样本预热 1 条、C4 全量测试；默认两轮 |
| summarize.py | 仅汇总无截断、Thinking/请求计数完整的全部正式请求；按总 wall 算吞吐 |
| stop.py / ops.py | receipt UID+PID+start ticks 校验，只停止该服务会话并确认端口/选卡释放 |
| check_environment.py | 不创建 CUDA context，检查记录包版本、Python 和所需可执行工具 |

默认物理卡 0、127.0.0.1:8000、state-dir=`.local/service`。GPU 是可移植参数，不是实验主机编号；禁止全局 pkill。使用非默认 state-dir 时，benchmark/stop 必须显式提供对应 --receipt。

这些是发布时新增的可移植包装脚本，沿用已发布方案的进程归属、工具链及模型校验；启动参数来自原生 N3 实测。仅做静态审查，本次未重新测 GPU 性能。实际原始 worker 与请求客户端另有来源 SHA 审计。

完整环境变量、启动/停止/测试顺序见 [实践方案](../readme.md)。
