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