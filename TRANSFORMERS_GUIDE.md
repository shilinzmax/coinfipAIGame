# Transformers.js 本地AI部署指南

## 🎯 概述

Transformers.js是一个在浏览器中直接运行AI模型的库，无需服务器，完全在本地运行。这是最简单、最轻量级的本地AI解决方案。

## ✨ 优势

- ✅ **完全本地**：在浏览器中运行，无需服务器
- ✅ **轻量级**：模型大小100-500MB
- ✅ **免费**：完全免费使用
- ✅ **简单**：一键加载，无需安装
- ✅ **跨平台**：支持所有现代浏览器

## 🚀 快速开始

### 步骤1：配置已就绪
你的游戏已经配置好了Transformers.js！无需额外设置。

### 步骤2：测试功能
1. 打开你的掷硬币游戏
2. 注册/登录账号
3. 玩几局游戏（至少3次）
4. 点击AI分析按钮
5. 等待模型加载（首次需要1-2分钟）

## 📊 支持的模型

### 当前配置
```javascript
transformers: {
    model: 'Xenova/distilbert-base-uncased', // 轻量级模型
    task: 'text-generation', // 文本生成任务
    maxLength: 200 // 最大生成长度
}
```

### 其他可选模型

#### 轻量级模型（推荐）
```javascript
// 1. DistilBERT (100MB)
model: 'Xenova/distilbert-base-uncased'

// 2. TinyBERT (50MB)
model: 'Xenova/tinybert-base-uncased'

// 3. MobileBERT (100MB)
model: 'Xenova/mobilebert-base-uncased'
```

#### 中等模型
```javascript
// 1. BERT Base (400MB)
model: 'Xenova/bert-base-uncased'

// 2. RoBERTa (500MB)
model: 'Xenova/roberta-base'
```

#### 文本生成模型
```javascript
// 1. GPT-2 Small (500MB)
model: 'Xenova/gpt2'

// 2. DistilGPT-2 (300MB)
model: 'Xenova/distilgpt2'
```

## 🔧 自定义配置

### 修改模型
在 `script.js` 中找到 `AI_CONFIG` 对象：

```javascript
const AI_CONFIG = {
    backend: 'transformers',
    transformers: {
        model: 'Xenova/your-preferred-model', // 修改这里
        task: 'text-generation',
        maxLength: 200
    }
};
```

### 调整参数
```javascript
transformers: {
    model: 'Xenova/distilbert-base-uncased',
    task: 'text-generation',
    maxLength: 300,        // 增加生成长度
    temperature: 0.8,      // 增加创造性
    topK: 50,             // 限制词汇选择
    topP: 0.9             // 核采样
}
```

## ⚡ 性能优化

### 模型选择建议

#### 低端设备（2-4GB RAM）
```javascript
model: 'Xenova/tinybert-base-uncased'  // 50MB
```

#### 中端设备（4-8GB RAM）
```javascript
model: 'Xenova/distilbert-base-uncased'  // 100MB
```

#### 高端设备（8GB+ RAM）
```javascript
model: 'Xenova/bert-base-uncased'  // 400MB
```

### 加载优化
```javascript
// 预加载模型（可选）
async function preloadModel() {
    try {
        await loadTransformersJS();
        const generator = await window.pipeline('text-generation', 'Xenova/distilbert-base-uncased');
        console.log('模型预加载完成！');
    } catch (error) {
        console.log('预加载失败，将在使用时加载');
    }
}

// 在页面加载时预加载
window.addEventListener('load', preloadModel);
```

## 🎮 使用体验

### 首次使用
1. **模型加载**：首次使用需要1-2分钟下载模型
2. **缓存机制**：模型会缓存在浏览器中，后续使用更快
3. **离线使用**：模型下载后可以离线使用

### 分析功能
- **游戏模式分析**：分析用户的游戏习惯
- **结果预测**：基于历史数据预测下次结果
- **个性化洞察**：提供游戏建议和统计

## 🛠️ 故障排除

### 常见问题

#### 1. 模型加载失败
```javascript
// 检查网络连接
console.log('检查网络连接...');

// 尝试备用模型
model: 'Xenova/tinybert-base-uncased'  // 更小的模型
```

#### 2. 内存不足
```javascript
// 使用更小的模型
model: 'Xenova/tinybert-base-uncased'  // 50MB

// 减少生成长度
maxLength: 100
```

#### 3. 生成质量不佳
```javascript
// 使用更大的模型
model: 'Xenova/bert-base-uncased'  // 400MB

// 调整参数
temperature: 0.7,
topK: 50,
topP: 0.9
```

### 调试模式
```javascript
// 启用详细日志
console.log('Transformers.js调试模式');

// 检查模型状态
if (window.pipeline) {
    console.log('Transformers.js已加载');
} else {
    console.log('Transformers.js未加载');
}
```

## 📱 浏览器兼容性

### 支持的浏览器
- ✅ Chrome 80+
- ✅ Firefox 75+
- ✅ Safari 13+
- ✅ Edge 80+

### 不支持的功能
- ❌ Internet Explorer
- ❌ 旧版移动浏览器

## 🔒 隐私和安全

### 数据隐私
- ✅ **完全本地**：所有数据在浏览器中处理
- ✅ **无网络传输**：分析过程不发送到服务器
- ✅ **用户控制**：用户可以完全控制数据

### 安全考虑
- ✅ **无API密钥**：不需要任何密钥
- ✅ **无服务器**：没有服务器被攻击的风险
- ✅ **沙盒环境**：在浏览器沙盒中运行

## 💡 高级用法

### 自定义提示词
```javascript
// 在callTransformers函数中自定义提示词
const customPrompt = `
你是一个专业的游戏数据分析师。
请分析以下游戏数据：${prompt}
请用中文回答，语言要生动有趣。
`;

const result = await generator(customPrompt, options);
```

### 批量分析
```javascript
// 分析多个用户的数据
async function analyzeMultipleUsers(users) {
    const results = [];
    for (const user of users) {
        const analysis = await callTransformers(user.gameData, config);
        results.push(analysis);
    }
    return results;
}
```

### 缓存优化
```javascript
// 缓存分析结果
const analysisCache = new Map();

async function getCachedAnalysis(userId, gameData) {
    const cacheKey = `${userId}_${JSON.stringify(gameData)}`;
    
    if (analysisCache.has(cacheKey)) {
        return analysisCache.get(cacheKey);
    }
    
    const analysis = await callTransformers(gameData, config);
    analysisCache.set(cacheKey, analysis);
    return analysis;
}
```

## 🎯 总结

Transformers.js是最简单的本地AI解决方案：

- **零配置**：无需安装任何软件
- **完全免费**：无任何费用
- **隐私安全**：数据不离开浏览器
- **跨平台**：支持所有现代浏览器
- **轻量级**：模型大小适中

现在你的掷硬币游戏已经具备了真正的AI分析能力！🎮🤖

## 🚀 开始使用

1. **打开游戏**：你的游戏已经配置好了
2. **开始游戏**：玩几局游戏
3. **AI分析**：点击AI分析按钮
4. **享受智能分析**：获得个性化的游戏洞察

无需任何额外设置，立即开始享受AI驱动的游戏体验！✨
