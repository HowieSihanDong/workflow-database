



### 地域与 CDP URL 对应表
随机IP：remote-192-168-1-43-9223 
土耳其：remote-192-168-1-58-9223
印度尼西亚：remote-192-168-1-59-9223

## 注意事项
- **元素 ID 动态变化**: 网页内容变化频繁，灵活使用snapshot和screenshot重新检查。
- 若页面文案存在中英文差异（例如“分析/Analytics”、“高级模式/Advanced mode”），同时尝试常见别名。
- 遇到动态渲染导致定位不稳时，优先使用可见文本定位（text selectors），备用 CSS/XPath 作为回退。

## 风控处理
**在两～三次操作之间，随机添加动作模拟鼠标移动、滚动、无效点击等操作，以避免被 YouTube 识别为机器人。** （具体措施你可以弄得很随机，主要为了反封控）
- 如果已经触发风控，请告知用户，稍后重试

## 子任务/Subagent的最佳实践
- 子任务会以subagent的方式进行实施，推荐使用 sessions_spawn 创建 subagent，每个子任务独立运行
- 不要用固定名命名subagent/subsession ，而是“任务名 + 时间戳/短随机串”
- 要求子任务尽量通过snapshot和screenshot(配合image_process)等方法，确认任务是否真的完成。
- 一个创建 subagent 时的调用模板在script目录下.