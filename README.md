# English Card Skill

一个用于批量制作「抖音风格英语单词卡片短视频」的 Codex Skill。

它沉淀了一个完整的视频生产流程：从词根、词缀、单词族、易混词脚本，到 Remotion 画面结构，再到阿里百炼 CosyVoice 配音、字幕同步、质量检查和最终导出。

## 适合做什么

- 英语词根短视频
- 单词拆解卡片
- 英语词缀/前缀/后缀记忆视频
- 易混词、发音、词义对比视频
- 黑黄高对比英语单词短片
- Remotion + TTS 批量视频模板

## 核心能力

- 将词根、词缀、单词列表、易混词或发音主题转成短视频脚本
- 生成抖音英语学习类快节奏口播结构
- 复用黑黄高对比视觉规则
- 使用阿里百炼 DashScope / CosyVoice 生成配音
- 根据真实音频时长生成字幕时间轴
- 用 Remotion 驱动画面、字幕、高亮词和 punch zoom
- 提供导出前质量检查清单

## 目录结构

```text
skills/douyin-remotion-video/
├─ SKILL.md
├─ workflow.md
├─ references/
├─ templates/
├─ prompts/
└─ examples/
```

## 快速使用

把 `skills/douyin-remotion-video` 放到你的 Codex Skills 目录，或在项目中直接引用它。

然后对 Codex 说：

```text
使用 douyin-remotion-video skill，帮我把这个英语词根/单词列表做成抖音风格 Remotion 短视频。
```

如果需要生成配音，请在本地环境变量中配置：

```powershell
$env:DASHSCOPE_API_KEY="你的 DashScope API Key"
```

注意：不要把 API Key 写进代码或提交到仓库。

## 推荐工作流

1. 写一期 `episode brief`
2. 生成 `voiceScript.ts`
3. 实现或复用 Remotion 组件
4. 调用 CosyVoice 生成分句音频
5. 合并为 `main-voice.mp3`
6. 生成 `generatedVoiceTimeline.ts`
7. 根据真实音频驱动画面和字幕
8. 渲染关键帧检查
9. 导出最终 MP4

完整步骤见：

[skills/douyin-remotion-video/workflow.md](skills/douyin-remotion-video/workflow.md)

## 示例

当前内置示例是 `-ject` 词根视频：

- reject
- object
- subject
- project
- inject
- eject
- abject
- deject

核心记忆点：

```text
ject = throw / 投出去
```

示例说明见：

[skills/douyin-remotion-video/examples/ject_episode_example.md](skills/douyin-remotion-video/examples/ject_episode_example.md)

## 设计风格

- 黑色背景
- 黄色关键词
- 白色中文解释
- 底部字幕条
- 大字 punch zoom
- 快速闪词
- 轻微粒子、光晕、扫描线
- 配音驱动字幕和画面节奏

## 安全说明

本仓库不包含任何 API Key。

使用 TTS 时，请通过环境变量传入：

```text
DASHSCOPE_API_KEY
```

## License

按仓库后续需要补充。
