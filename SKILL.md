---
name: "workflow-database"
description: "社交平台自动化操作 Skill。触发条件：(1) 用户提及上传 YouTube/Facebook 视频 + 指定地域浏览器；(2) 用户要求回复/提取 YouTube 评论或数据；(3) 用户指定 '随机IP/土耳其/印尼浏览器' 地域 + 任务指令。执行 YouTube 上传、评论回复、数据提取、Facebook Reels 上传等操作。"
---

# 🛠 现有工作流
- **YouTube 上传与发布** (/resources/youtube-upload.md): 自动化视频上传、填写元数据及公开发布。
- **YouTube 频道数据分析导出** (/resources/youtube-data-extract.md): 自动进入分析后台并提取关键指标。
- **YouTube 评论回复** (/resources/youtube-comment.md): 自动回复 YouTube 评论，保持互动性。
- **Facebook Reels 上传 & 发布** (/resources/fb-reels-upload.md): 自动上传 Reels 视频到 Facebook 平台。
- **通用提示 & 注意事项** (rule-and-tips.md): 包含一些通用提示 & 要求，帮助智能体在执行任务时避免常见错误。地域与 Chrome Profile 的 CDP URL 对应表也包含其中。

# 常用配合Skill
- browser （优先使用）
- image_process