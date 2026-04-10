# 📤 视频上传的完整 Browser 工具调用流程（成功例子）

## 步骤 1：先下载视频到本地

```json
{
  "name": "exec",
  "parameters": {
    "command": "mkdir -p /tmp/openclaw/uploads && curl -s -L 'https://howie.tos-cn-beijing.volces.com/new.mp4' -o /tmp/openclaw/uploads/video.mp4 && ls -lh /tmp/openclaw/uploads/video.mp4"
  }
}
```

## 步骤 2：检查并启动浏览器（如果需要）

检查浏览器是否运行：

```json
{
  "name": "exec",
  "parameters": {
    "command": "lsof -i :9222 || netstat -tlnp 2>/dev/null | grep 9222 || ss -tlnp | grep 9222 || echo 'Browser not running'"
  }
}
```

如果没运行，启动浏览器：

```json
{
  "name": "exec",
  "parameters": {
    "command": "bash /opt/browser-vnc/start-chromium.sh"
  }
}
```

## 步骤 3：打开 YouTube Studio

```json
{
  "name": "browser",
  "parameters": {
    "action": "open",
    "url": "https://studio.youtube.com/",
    "profile": "remote-192-168-1-59-9223"
  }
}
```

## 步骤 4：获取页面结构

```json
{
  "name": "browser",
  "parameters": {
    "action": "snapshot"
  }
}
```

## 步骤 5：点击"创建"按钮

假设从 snapshot 中拿到"创建"按钮的 ref 是 e5：

```json
{
  "name": "browser",
  "parameters": {
    "action": "act",
    "request": {
      "kind": "click",
      "ref": "e5"
    },
    "profile": "remote-192-168-1-59-9223"
  }
}
```

## 步骤 6：点击"上传视频"

重新 snapshot 找到"上传视频"按钮：

```json
{
  "name": "browser",
  "parameters": {
    "action": "snapshot",
    "interactive": true
  }
}
```

假设"上传视频"按钮的 ref 是 e8：

```json
{
  "name": "browser",
  "parameters": {
    "action": "act",
    "request": {
      "kind": "click",
      "ref": "e8"
    },
    "profile": "remote-192-168-1-59-9223"
  }
}
```

## 步骤 7：上传文件（关键步骤！）

### 方式 A：直接使用 upload action（推荐）

```json
{
  "name": "browser",
  "parameters": {
    "action": "upload",
    "paths": ["/tmp/openclaw/uploads/video.mp4"],
    "inputRef": "e10",
    "profile": "remote-192-168-1-59-9223"
  }
}
```

### 方式 B：先点击文件选择按钮，再处理（不推荐）

不推荐原因：会触发系统级文件选择弹窗，无法自动化。

```json
{
  "name": "browser",
  "parameters": {
    "action": "act",
    "request": {
      "kind": "click",
      "ref": "e10"
    },
    "profile": "remote-192-168-1-59-9223"
  }
}
```

## 步骤 8：填写标题

等待上传弹窗出现后 snapshot：

```json
{
  "name": "browser",
  "parameters": {
    "action": "snapshot",
    "interactive": true
  }
}
```

找到标题输入框，假设 ref 是 e15：

```json
{
  "name": "browser",
  "parameters": {
    "action": "act",
    "request": {
      "kind": "type",
      "ref": "e15",
      "text": "神秘的中国技术"
    },
    "profile": "remote-192-168-1-59-9223"
  }
}
```

## 步骤 9：继续后续流程

点击"继续"按钮（多次）：

```json
{
  "name": "browser",
  "parameters": {
    "action": "act",
    "request": {
      "kind": "click",
      "ref": "e20"
    },
    "profile": "remote-192-168-1-59-9223"
  }
}
```

重复点击"继续"直到发布页面。

设置为公开：

```json
{
  "name": "browser",
  "parameters": {
    "action": "act",
    "request": {
      "kind": "click",
      "ref": "e30"
    },
    "profile": "remote-192-168-1-59-9223"
  }
}
```

点击"发布"按钮：

```json
{
  "name": "browser",
  "parameters": {
    "action": "act",
    "request": {
      "kind": "click",
      "ref": "e35"
    },
    "profile": "remote-192-168-1-59-9223"
  }
}
```

---

# 🔑 关键点总结

1. **文件必须在正确位置**：`/tmp/openclaw/uploads/`

2. **推荐使用 upload action**：
   ```json
   {
     "action": "upload",
     "paths": ["/tmp/openclaw/uploads/video.mp4"],
     "inputRef": "e10"
   }
   ```

3. **不要直接点击"选择文件"按钮**：
   - ❌ 会触发系统级文件选择弹窗，无法自动化
   - ✅ 直接用 upload action 注入文件

4. **注意 profile 参数**：每个 browser 调用都要指定 profile（如果用远程浏览器）
5. 这只是个例子，你自己借鉴和反思即可。
