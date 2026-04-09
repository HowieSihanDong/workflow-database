## 何时使用
用户要求“分析/提取 YouTube 数据/指标/表格/高级模式”等任务时，用于从youtube分析数据中提取指标。

## 前置输入
- 可选：视频名字（如：Algorithm Visualization - Search Comparison），也可以看全部视频数据
- 可选：时间范围、细分维度等信息
- 必填：需要查询的指标清单
- 可选：使用的浏览器

## 用户输入举例
我现在要分析我发的youtube视频数据，帮我拿一下数据
浏览器：南非（能够根据南非找到cdpurl）
视频名字：Algorithm Visualization - Search Comparison
数据：
    - 观看次数（默认选中）
    - 感兴趣的观看次数
    - 观看时长（小时）（默认选中）
    - 订阅人数（默认选中）
    - 平均观看时长（默认选中）
    - 平均观看百分比
    - 添加的视频数
    - 发布的视频数


## 大致步骤
1. 使用用户指定浏览器，打开 https://studio.youtube.com/（全程仅在 `studio.youtube.com` 域内操作，不打开其他网站或外链。）
2. 找到做侧边栏“数据分析”
3. 打开“高级模式“
4. 根据用户需求，参考/references/params.md中的指标，确认点击策略
5. 拿到目标数据结果，以表格格式返回指标数据
6. 结果保存到`/root/<今日时间（yyyy-MM-dd-HH:mm:ss）>.md`文件中