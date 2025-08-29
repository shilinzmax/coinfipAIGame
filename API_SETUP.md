# 🔑 API密钥配置指南

## 概述
为了保护API密钥安全，项目使用配置文件来管理敏感信息。

## 📁 文件结构

```
├── config.example.js        # 配置文件示例（包含占位符）
├── config.js               # 本地配置文件（需要创建，包含真实密钥）
├── .gitignore              # Git忽略文件（保护敏感信息）
└── index.html              # 主页面（引入配置文件）
```

## 🚀 设置步骤

### 1. 创建本地配置文件
```bash
# 复制示例文件
cp config.example.js config.js
```

### 2. 编辑本地配置文件
打开 `config.js` 并填入真实的API密钥：

```javascript
window.API_CONFIG = {
    // OpenAI API密钥
    OPENAI_API_KEY: 'sk-your-openai-api-key-here',
    
    // Hugging Face API密钥
    HUGGINGFACE_API_KEY: 'hf-your-huggingface-api-key-here',
    
    // Claude API密钥
    CLAUDE_API_KEY: 'sk-ant-your-claude-api-key-here',
    
    // Gemini API密钥
    GEMINI_API_KEY: 'your-gemini-api-key-here'
};
```

### 3. 获取API密钥

#### OpenAI API
1. 访问 [OpenAI Platform](https://platform.openai.com/api-keys)
2. 创建API密钥
3. 复制密钥到配置文件

#### Hugging Face API
1. 访问 [Hugging Face Settings](https://huggingface.co/settings/tokens)
2. 创建Classic Token
3. 复制密钥到配置文件

#### Claude API
1. 访问 [Anthropic Console](https://console.anthropic.com/)
2. 创建API密钥
3. 复制密钥到配置文件

#### Gemini API
1. 访问 [Google AI Studio](https://makersuite.google.com/app/apikey)
2. 创建API密钥
3. 复制密钥到配置文件

## 🔒 安全说明

### ✅ 安全做法
- ✅ `config.js` 已添加到 `.gitignore`
- ✅ 不会提交到远程仓库
- ✅ 使用示例文件作为模板

### ❌ 避免的做法
- ❌ 不要在代码中硬编码API密钥
- ❌ 不要提交包含真实密钥的文件
- ❌ 不要在公共仓库中暴露密钥

## 🎯 使用示例

### 切换AI后端
在 `script.js` 中修改：

```javascript
const AI_CONFIG = {
    backend: 'openai', // 可选: 'openai', 'huggingface', 'claude', 'gemini'
    // ...
};
```

### 测试配置
1. 打开浏览器控制台
2. 输入：`console.log(window.API_CONFIG)`
3. 检查密钥是否正确加载

## 🚀 部署到远程

### GitHub Pages
1. 确保 `config.local.js` 在 `.gitignore` 中
2. 推送代码到GitHub
3. 在GitHub Pages设置中配置环境变量（如果支持）

### Netlify
1. 在Netlify控制台中设置环境变量
2. 使用构建脚本来生成配置文件

### Vercel
1. 在Vercel控制台中设置环境变量
2. 使用构建脚本来生成配置文件

## 🆘 故障排除

### 问题：API密钥未加载
**解决方案：**
1. 检查 `config.js` 是否存在
2. 检查文件路径是否正确
3. 检查浏览器控制台是否有错误

### 问题：API调用失败
**解决方案：**
1. 检查API密钥是否正确
2. 检查API服务是否可用
3. 检查网络连接

## 📞 支持

如果遇到问题，请检查：
1. 浏览器控制台错误信息
2. 网络请求状态
3. API服务状态页面
