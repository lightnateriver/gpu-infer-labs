# 独立性能报告

下载并用浏览器打开 [report.html](report.html)。GitHub 的文件页通常展示源码；报告不依赖网络、外部资源或其他 HTML。

内容包括卡型/版本、3.024 条/分钟与 238.54 token/s/卡、TTFT/TPOT/E2E、逐轮及匿名逐样本性能、吞吐柱状图、FP8/Graph/async/KV 配置和输入/计时方法，并保留同配置复测波动与精度边界。

重建方式（只读取随包匿名数据，不运行推理）：

```bash
python3 report/build_report.py
```

报告不包含原业务 Caption、完整 prompt、私有数据来源或机器登录信息。真实输入和启动/测试方法见 [方案说明](../readme.md)。
