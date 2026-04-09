---
name: "workflow-database"
description: "`workflow-database` 是一个流程知识库，旨在为智能体提供针对特定平台（如 YouTube）的标准化操作流程。它通过结合 CDP/Playwright 技能，实现自动化的网页交互任务。"
---

# 🛠 现有工作流
- **YouTube 上传与发布**(/resources/youtube-upload.md): 自动化视频上传、填写元数据及公开发布。resources/youtube-upload.md
- **YouTube 频道数据分析导出**(/resources/youtube-data-extract.md): 自动进入分析后台并提取关键指标。resources/youtube-data-extract.md
- **YouTube 评论回复**(/resources/youtube-comment.md): 自动回复 YouTube 评论，保持互动性。resources/youtube-comment.md
- **Facebook Reels 上传 & 发布**(/resources/fb-reels-upload.md): 自动上传 Reels 视频到 Facebook 平台。 resources/fb-reels-upload.md
- /resources/tips.md：这是一个包含一些通用提示的文件，用于帮助智能体在执行任务时避免常见错误。(也包含了，地域和chrome profile的匹配信息，你可以在这里查找)
- /resources/openclaw_cli_reference.md：这是一个包含一些通用CDP/Playwright操作的文件，帮助智能体快速定位元素、执行操作等。

# 注意事项
- **元素 ID 动态变化**: 网页元素的 ref ID 可能会随页面更新而变化。如果操作失败，灵活执行 snapshot和screenshot重新检查元素。
- 不必等待页面完全加载；可见即点、可见即取。
- CDP/网络不稳时，需要自动重试至少3次
- 若页面文案存在中英文差异（例如“分析/Analytics”、“高级模式/Advanced mode”），同时尝试常见别名。
- 遇到动态渲染导致定位不稳时，优先使用可见文本定位（text selectors），备用 CSS/XPath 作为回退。


## 子任务/Subagent的最佳实践
- 子任务会以subagent的方式进行实施。因此，要求子任务尽量通过snapshot和screenshot(配合image_process)等方法，必须确认任务是否真的完成。

You MUST send active progress reports to the main agent FREQUENTLY:
- Send a progress update EVERY 30 SECONDS or EVERY 1 STEP COMPLETED
- Use this exact format:
  [progress] runId={runId} percent={N}% info="what you are doing now"

DO NOT FINISH WITHOUT REPORTING.
Main agent will NOT consider you done until it sees multiple progress updates + final done message.