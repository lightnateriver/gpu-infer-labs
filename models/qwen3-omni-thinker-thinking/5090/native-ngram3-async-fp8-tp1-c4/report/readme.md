# 独立性能报告

打开本目录 report.html 即可查看；没有外部 JS/CSS、网络字体、关联 HTML 或私有媒体。浅色红系，包含吞吐柱状图、每卡 TPS、TTFT/TPOT/E2E、逐轮与 90 条匿名指标、接受率、输入定义、配置变化及质量边界。

```bash
python3 report/build_report.py
```

从 ../evidence/results.json 重建；生成不访问 GPU，也不是新一轮性能测试。N3 的 2.27% 任务吞吐增益是两轮记录，未证明稳定生产收益；N5 不作为推荐配置。

[返回方案说明](../readme.md)
