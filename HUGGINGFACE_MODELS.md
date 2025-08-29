# 🤗 Hugging Face 可用模型列表

## 推荐的可用模型

### 1. GPT-2 系列（推荐）
```javascript
model: 'gpt2'                    // 基础GPT-2模型
model: 'distilgpt2'              // 轻量级GPT-2
model: 'gpt2-medium'             // 中等大小GPT-2
```

### 2. 对话模型
```javascript
model: 'microsoft/DialoGPT-small'    // 小版本对话模型
model: 'facebook/blenderbot-400M-distill'  // Facebook对话模型
```

### 3. 文本生成模型
```javascript
model: 'EleutherAI/gpt-neo-125M'     // 开源GPT模型
model: 'microsoft/DialoGPT-medium'   // 如果可用的话
```

## 如何测试模型

在浏览器控制台中运行：
```javascript
// 测试不同模型
AI_CONFIG.huggingface.model = 'gpt2';
testHuggingFaceAPI();

// 或者测试其他模型
AI_CONFIG.huggingface.model = 'distilgpt2';
testHuggingFaceAPI();
```

## 模型特点

| 模型 | 大小 | 速度 | 质量 | 推荐场景 |
|------|------|------|------|----------|
| gpt2 | 117M | 快 | 好 | 通用文本生成 |
| distilgpt2 | 82M | 很快 | 中等 | 快速响应 |
| gpt2-medium | 345M | 中等 | 很好 | 高质量生成 |
| DialoGPT-small | 117M | 快 | 好 | 对话场景 |

## 故障排除

### 404错误
- 模型名称不正确
- 模型不在Inference API中
- 尝试其他模型

### 503错误
- 模型正在加载
- 等待几分钟后重试

### 401错误
- API密钥无效
- 检查密钥权限
