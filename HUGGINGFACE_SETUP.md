# 🤗 Hugging Face AI集成指南

## 概述
本指南将帮助你设置Hugging Face API来改进掷硬币游戏的AI分析功能。

## 🚀 快速开始

### 1. 获取Hugging Face API密钥

1. 访问 [Hugging Face官网](https://huggingface.co/)
2. 注册账号或登录
3. 进入 [Settings > Access Tokens](https://huggingface.co/settings/tokens)
4. 点击 "New token"
5. 选择 "Read" 权限（免费）
6. 复制生成的API密钥

### 2. 配置API密钥

在 `script.js` 文件中找到以下配置：

```javascript
huggingface: {
    apiKey: 'YOUR_HUGGINGFACE_API_KEY', // 替换为你的API密钥
    model: 'microsoft/DialoGPT-medium',
    baseUrl: 'https://api-inference.huggingface.co/models',
    maxLength: 200,
    temperature: 0.7
}
```

将 `YOUR_HUGGINGFACE_API_KEY` 替换为你的实际API密钥。

## 🎯 推荐的模型

### 对话模型（推荐用于游戏分析）
- `microsoft/DialoGPT-medium` - 中等大小，适合对话分析
- `microsoft/DialoGPT-small` - 较小，响应更快
- `microsoft/DialoGPT-large` - 更大，分析更深入

### 文本生成模型
- `gpt2` - 经典文本生成模型
- `distilgpt2` - 轻量级版本
- `EleutherAI/gpt-neo-125M` - 开源GPT模型

### 专门的分析模型
- `facebook/blenderbot-400M-distill` - 对话和分析
- `microsoft/DialoGPT-medium` - 最适合游戏分析

## 🔧 配置选项

### 模型参数
```javascript
huggingface: {
    apiKey: 'your-api-key',
    model: 'microsoft/DialoGPT-medium', // 选择模型
    baseUrl: 'https://api-inference.huggingface.co/models',
    maxLength: 200,        // 最大生成长度
    temperature: 0.7,      // 创造性 (0.1-1.0)
    top_p: 0.9,           // 核采样
    repetition_penalty: 1.1 // 重复惩罚
}
```

### 参数说明
- `maxLength`: 控制生成文本的最大长度
- `temperature`: 控制创造性，越高越随机
- `top_p`: 核采样，控制词汇选择的多样性
- `repetition_penalty`: 防止重复，>1.0减少重复

## 💡 使用技巧

### 1. 优化提示词
为Hugging Face模型设计专门的提示词：

```javascript
// 游戏分析提示词
const gameAnalysisPrompt = `
你是一个专业的游戏数据分析师。请分析以下掷硬币游戏数据：

用户: ${user.username}
游戏次数: ${gameHistory.length}
正面次数: ${headsCount}
反面次数: ${tailsCount}

请提供：
1. 游戏模式分析
2. 趋势预测
3. 个性化建议

请用中文回答，语言要生动有趣。
`;
```

### 2. 错误处理
```javascript
// 在callHuggingFace函数中
if (response.status === 503) {
    // 模型正在加载，等待后重试
    await new Promise(resolve => setTimeout(resolve, 5000));
    return await callHuggingFace(prompt, config);
}
```

### 3. 缓存结果
```javascript
// 缓存API结果以提高性能
const cache = new Map();
const cacheKey = `${model}-${prompt.substring(0, 50)}`;
if (cache.has(cacheKey)) {
    return cache.get(cacheKey);
}
```

## 🆓 免费使用限制

### Hugging Face免费层限制
- 每月1000次请求
- 每次请求最大512 tokens
- 部分模型需要等待加载

### 优化建议
1. 使用较小的模型（如DialoGPT-small）
2. 实现请求缓存
3. 合并多个分析请求
4. 设置请求频率限制

## 🔄 模型切换

你可以轻松切换不同的模型：

```javascript
// 切换到更快的模型
huggingface: {
    model: 'microsoft/DialoGPT-small',
    // ... 其他配置
}

// 切换到更强大的模型
huggingface: {
    model: 'microsoft/DialoGPT-large',
    // ... 其他配置
}
```

## 🐛 常见问题

### Q: API返回503错误
A: 模型正在加载，等待几秒后重试

### Q: 生成的内容质量不高
A: 尝试调整temperature参数或使用更大的模型

### Q: 请求超时
A: 减少maxLength参数或使用更小的模型

### Q: API密钥无效
A: 检查密钥是否正确，确保有Read权限

## 📊 性能对比

| 模型 | 大小 | 速度 | 质量 | 推荐场景 |
|------|------|------|------|----------|
| DialoGPT-small | 117M | 快 | 中等 | 快速响应 |
| DialoGPT-medium | 345M | 中等 | 好 | 平衡选择 |
| DialoGPT-large | 774M | 慢 | 很好 | 深度分析 |

## 🎉 开始使用

1. 获取API密钥
2. 更新配置
3. 测试AI分析功能
4. 根据需要调整模型和参数

现在你的掷硬币游戏就有了强大的AI分析能力！🚀
