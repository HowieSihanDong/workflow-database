# 通用操作提示

## 日志过滤
所有指令添加 `--log-level error` 以减少上下文噪音：
```bash
openclaw browser click e14 --log-level error --browser-profile <chromeID>
```

## 浏览器实例指定
所有指令都显式指定浏览器实例，使用 `--browser-profile` 参数：

```bash
--browser-profile remote-192-168-1-58-9223

openclaw browser  --browser-profile remote-192-168-1-43-9223  snapshot 

openclaw browser snapshot --interactive --browser-profile remote-192-168-1-58-9223
```
这些command可能会出错（因为顺序，参数各种原因）。

如果出错，同步使用 browser 工具，例如:
-  "upload" 直接上传文件
- 使用 browser 工具的 action: "act" + request: { kind: "click" } 来点击按钮
- 使用 browser 工具的 action: "act" + request: { kind: "type" } 来输入标题和描述。
换言之，CLI或者browser工具都可以完成，你要敏捷快速的判断，做出最佳实践。

### 一个拼凑正确的指令示例
```bash
openclaw browser click e14 --browser-profile remote-192-168-1-58-9223
```

### 地域与 CDP URL 对应表

随机IP：remote-192-168-1-43-9223 
土耳其：remote-192-168-1-58-9223
印度尼西亚：remote-192-168-1-59-9223

## Tabs 操作

```bash
openclaw browser tabs                          # 列出所有 Tab
openclaw browser focus E78CDE3D9D5CCB48A8FE66B5B6897766  # 聚焦目标 Tab
```