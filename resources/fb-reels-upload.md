## 何时使用
- 当用户需要上传 Reels 视频到 Facebook 平台时，使用此工作流。

## 流程：Facebook Reels 上传 & 发布
1. 使用用户指定浏览器，打开 https://www.facebook.com/ （全程仅在 `www.facebook.com` 域内操作，不打开其他网站或外链。）
2. 进入顶部的 button "Facebook 菜单" 
2. button "Reels" 
3. 文件上传 【记住以下的操作必须连续，不能单独按上传视频button！】
    - mkdir -p /tmp/openclaw/uploads
    - curl -L 'url' -o /tmp/openclaw/uploads/video.mp4 [这里替换为视频下载链接]
    - ls -lh /tmp/openclaw/uploads/video.mp4
    - openclaw browser upload /tmp/openclaw/uploads/video.mp4 
    - button "为 Reels 上传视频"：openclaw browser evaluate --fn '(el) => el.click()' --ref e14 
【这里有个关键逻辑：直接点击该按钮会触发系统级文件选择弹窗，此弹窗会覆盖 Chrome 页面且无法被脚本操作。因此不能跳过前置步骤直接点击，必须先完成前四步操作，再执行点击。】
4. 不断点击 button "继续" ，输入 textbox 作为标题，最终发布 

## 额外任务（for上传任务ONLY【facebook上传和youtube上传】）
对于每一个上传任务，root目录存一个dramadata.md文件(/root/dramadata.md)，用于存储任务的元数据。表头为：地域 - 平台 - 视频名称。（如果没有dramadata.md文件，则创建一个）