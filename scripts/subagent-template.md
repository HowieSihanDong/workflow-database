## Subagent 创建模板

### 通用模板

```javascript
{
  "name": "sessions_spawn",
  "parameters": {
    "task": "使用 workflow-database skill 完成 {{任务描述}}：\n\n## 任务配置\n{{任务配置}}\n\n## 执行步骤\n1. 根据任务配置完成相应操作\n2. 完成后确认任务完成",
    "label": "{{任务标签}}",
    "runtime": "subagent",
    "mode": "run"
  }
}
```

### 使用示例（不一定非要这样）

**YouTube 评论回复**

- {{任务描述}}：YouTube 评论回复任务
- {{任务配置}}：
  - **地域**：{{地域}}
  - **Chrome Profile**：{{Chrome Profile}}
  - **目标视频**：{{视频名称}}
  - **回复要求**：{{回复要求}}

**YouTube 视频上传**

- {{任务描述}}：YouTube 视频上传任务
- {{任务配置}}：
  - **地域**：{{地域}}
  - **Chrome Profile**：{{Chrome Profile}}
  - **视频链接**：{{视频链接}}
  - **视频标题**：{{视频标题}}

**YouTube 数据分析**
- {{任务描述}}：YouTube 数据分析任务
- {{任务配置}}：
  - **地域**：{{地域}}
  - **Chrome Profile**：{{Chrome Profile}}
  - **目标视频**：{{视频名称}}
  - **时间范围**：{{时间范围}}
  - **分析指标**：{{指标列表}}

Note. label 就是给任务的"标题"或"备注"，方便你记住这个会话是干嘛的。你可以简单写写。不是必须。