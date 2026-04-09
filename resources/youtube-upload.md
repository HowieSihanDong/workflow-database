## 何时使用
用户要求“上传 YouTube 视频”等任务时，用于自动化视频上传、填写元数据及公开发布。

## 流程：YouTube视频上传 & 发布
在开始执行脚本前，请确认以下信息的完整性：
1. **视频下载链接**：缺失时需引导用户提供。
2. **视频标题**： 若缺失，应询问用户或告知将使用文件名作为标题。
3. **视频描述**： 若缺失，可保持为空或使用 AI 生成的简要说明，并告知用户。

📝 执行步骤（按顺序）
- 使用用户指定浏览器，打开 https://studio.youtube.com/ （全程仅在 `studio.youtube.com` 域内操作，不打开其他网站或外链。）
- button "创建" 
- button "上传视频" 
- 进入上传视频弹窗，上传视频文件：
    - mkdir -p /tmp/openclaw/uploads
    - curl -s -L '视频链接' -o /tmp/openclaw/uploads/video.mp4
    - ls -lh /tmp/openclaw/uploads/video.mp4
    - openclaw browser upload /tmp/openclaw/uploads/video.mp4 --log-level error --browser-profile <chromeID>
    - button "选择文件" 
    - 【这里有个关键逻辑：直接点击该按钮会触发系统级文件选择弹窗，此弹窗会覆盖 Chrome 页面且无法被脚本操作。因此不能跳过前置步骤直接点击，必须先完成前四步操作，再执行点击。】

- 进入发布流程弹窗的第一个page：输入标题、描述、设置内容不面向儿童、点击 "继续" 
- 进入发布流程弹窗的第二个page：点击 "继续" 
- 进入发布流程弹窗的第三个page：点击 "继续"
- 进入发布流程弹窗的第四个page：
    - 点击radio "公开"（设置为公开视频）、点击button "发布"
- 关闭正在上传的提醒弹窗

注意：上述的流程提到的button/ID的偏差，请根据实际情况调整。

## 额外任务（for上传任务ONLY）
对于每一个上传任务，root目录存一个dramadata.md文件，用于存储任务的元数据：存 地域 - 平台 - 视频名称。（如果没有，则创建一个）

