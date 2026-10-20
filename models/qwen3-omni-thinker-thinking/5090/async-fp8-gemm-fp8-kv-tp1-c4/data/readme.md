# 自备冻结性能输入

公开仓库不包含业务视频、参考图、完整 system prompt、shot plan、原始 Caption 或原数据来源。`manifest.example.json` 仅说明输入结构，里面的哈希占位符不能直接用于实测。

运行环境需要两棵外部目录：

```text
$DATA_DIR/
  <sample_id>/
    video.mp4
    img01.png
    img02.png
    img03.png
    ...                    # 原目录有 4–5 张时全部使用
$PREPARED_DIR/
  manifest.json
  <prepared_subdir>/
    system-prompt.txt       # 已冻结的完整最终 system 输入，含原运行时 context
    runtime-context.json   # 原冻结镜头表与运行时 JSON，保留以供核查
```

manifest 为列表，字段合同见 example：sample_id、prepared_subdir、reference_images（picture_id/file/sha256）、video_sha256、system_prompt_sha256、duration_seconds、reference_count、shot_count。媒体路径在 sample 目录下，客户端读取 `video.mp4`。`system-prompt.txt` 是实际发送的最终 system 字符串；客户端不会重新切镜头或改写 prompt。

不要以新自动切分覆盖原 shot plan 后声称复现旧输入。获得有权限的原冻结准备目录可直接使用；不同数据可按合同自备最终 prompt/镜头表并计算哈希，但性能数值不直接对照本目录 3.024。

原测试是 3 组各 5 条、视频约 12–15 秒、全部 3–5 参考图、同步音轨、2 fps。每轮输入 419,460 tokens。RTX 5090 TP1/C4、vLLM/vLLM-Omni 0.30.0；测试命令和完整指标见 [方案说明](../readme.md)。
