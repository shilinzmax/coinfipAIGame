# 🤖 AI模型详细说明

## 📊 当前模型分类

### 🏠 本地/内置模型（无需第三方服务）

#### 1. 🧠 智能分析（推荐）
- **类型**：内置算法
- **工作原理**：结合多种统计和模式识别算法
- **优势**：快速、准确、无需网络
- **数据需求**：需要游戏历史数据

#### 2. 📊 统计分析
- **类型**：内置算法
- **工作原理**：基于概率统计和贝叶斯分析
- **优势**：数学严谨、可解释性强
- **数据需求**：需要游戏历史数据

#### 3. 🔍 模式识别
- **类型**：内置算法
- **工作原理**：识别游戏中的重复模式和规律
- **优势**：能发现隐藏模式
- **数据需求**：需要至少3次游戏记录

#### 4. 🎲 随机预测
- **类型**：内置算法
- **工作原理**：完全随机预测，模拟真实硬币
- **优势**：简单、快速
- **数据需求**：无需数据

#### 5. 📈 趋势分析
- **类型**：内置算法
- **工作原理**：分析游戏趋势和波动性
- **优势**：能预测趋势变化
- **数据需求**：需要至少5次游戏记录

### 🌐 第三方服务模型

#### 6. 🤖 Transformers.js
- **类型**：浏览器内AI模型
- **工作原理**：在浏览器中运行轻量级AI模型
- **优势**：真正的AI，无需API密钥
- **限制**：模型较小，功能有限
- **数据需求**：无需数据

#### 7. 🦙 Ollama（本地AI）
- **类型**：本地AI服务
- **工作原理**：在本地运行AI模型
- **优势**：完全本地化，隐私安全
- **要求**：需要安装Ollama软件
- **数据需求**：无需数据

#### 8. 🧠 OpenAI GPT
- **类型**：云端AI服务
- **工作原理**：调用OpenAI API
- **优势**：功能强大，分析深入
- **要求**：需要OpenAI API密钥
- **费用**：按使用量付费
- **数据需求**：无需数据

#### 9. 🤖 Claude
- **类型**：云端AI服务
- **工作原理**：调用Anthropic Claude API
- **优势**：分析能力强，安全性高
- **要求**：需要Claude API密钥
- **费用**：按使用量付费
- **数据需求**：无需数据

#### 10. 🌟 Google Gemini
- **类型**：云端AI服务
- **工作原理**：调用Google Gemini API
- **优势**：Google的先进AI技术
- **要求**：需要Gemini API密钥
- **费用**：按使用量付费
- **数据需求**：无需数据

## 🔧 如何启用第三方服务

### 1. Transformers.js（推荐，免费）
```javascript
// 在script.js中修改AI_CONFIG
const AI_CONFIG = {
    backend: 'transformers', // 已经是默认设置
    transformers: {
        model: 'Xenova/distilbert-base-uncased',
        task: 'text-generation',
        maxLength: 200
    }
};
```

### 2. OpenAI GPT
```javascript
// 在script.js中修改AI_CONFIG
const AI_CONFIG = {
    backend: 'openai',
    openai: {
        apiKey: 'your-actual-openai-api-key', // 替换为真实密钥
        model: 'gpt-3.5-turbo'
    }
};
```

### 3. Claude
```javascript
// 在script.js中修改AI_CONFIG
const AI_CONFIG = {
    backend: 'claude',
    claude: {
        apiKey: 'your-actual-claude-api-key', // 替换为真实密钥
        model: 'claude-3-sonnet-20240229'
    }
};
```

### 4. Google Gemini
```javascript
// 在script.js中修改AI_CONFIG
const AI_CONFIG = {
    backend: 'gemini',
    gemini: {
        apiKey: 'your-actual-gemini-api-key', // 替换为真实密钥
        model: 'gemini-pro'
    }
};
```

### 5. Ollama（本地）
```javascript
// 在script.js中修改AI_CONFIG
const AI_CONFIG = {
    backend: 'ollama',
    ollama: {
        baseUrl: 'http://localhost:11434',
        model: 'tinyllama'
    }
};
```

## 💰 费用对比

| 服务 | 费用 | 优势 | 劣势 |
|------|------|------|------|
| **内置算法** | 免费 | 快速、隐私 | 功能有限 |
| **Transformers.js** | 免费 | 真正AI、无需密钥 | 模型较小 |
| **Ollama** | 免费 | 本地化、隐私 | 需要安装软件 |
| **OpenAI** | 付费 | 功能强大 | 需要API密钥 |
| **Claude** | 付费 | 分析深入 | 需要API密钥 |
| **Gemini** | 付费 | Google技术 | 需要API密钥 |

## 🎯 推荐配置

### 初学者（免费）
```javascript
const AI_CONFIG = {
    backend: 'transformers' // 使用Transformers.js
};
```

### 专业用户（付费）
```javascript
const AI_CONFIG = {
    backend: 'openai' // 使用OpenAI GPT
};
```

### 隐私优先（本地）
```javascript
const AI_CONFIG = {
    backend: 'ollama' // 使用本地Ollama
};
```

## 🔄 当前状态

**当前配置**：`backend: 'transformers'`
- ✅ 使用Transformers.js（浏览器内AI）
- ✅ 免费，无需API密钥
- ✅ 真正的AI模型
- ⚠️ 模型较小，功能有限

**其他模型**：
- 🏠 智能分析、统计分析等：内置算法，免费
- 🌐 OpenAI、Claude、Gemini：需要API密钥和付费
- 🦙 Ollama：需要本地安装

## 🚀 如何切换模型

1. **修改配置**：在`script.js`中修改`AI_CONFIG.backend`
2. **添加API密钥**：如果使用付费服务，需要添加真实的API密钥
3. **重新加载页面**：刷新浏览器页面

## 💡 建议

- **新手**：使用Transformers.js（当前默认）
- **有预算**：使用OpenAI GPT
- **隐私要求高**：使用Ollama
- **免费且功能强**：使用内置智能分析算法
