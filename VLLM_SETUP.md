# vLLM 部署指南

## 🤖 为掷硬币游戏集成 vLLM AI 分析

你的掷硬币游戏现在支持 AI 智能分析！本指南将帮助你部署 vLLM 来提供真实的 AI 推理功能。

## 📋 当前状态

- ✅ **模拟AI分析**：默认使用智能模拟数据
- ✅ **多后端支持**：支持 vLLM、OpenAI、Claude、Gemini
- ✅ **完整UI**：美观的AI分析界面
- ✅ **智能分析**：游戏模式识别、结果预测、个性化洞察

## 🚀 vLLM 部署选项

### 选项1：本地部署 vLLM (推荐)

#### 1. 安装 vLLM
```bash
# 安装 vLLM
pip install vllm

# 或者使用 conda
conda install -c conda-forge vllm
```

#### 2. 启动 vLLM 服务
```bash
# 使用 Llama-2 模型
python -m vllm.entrypoints.openai.api_server \
    --model meta-llama/Llama-2-7b-chat-hf \
    --port 8000 \
    --host 0.0.0.0

# 或者使用其他模型
python -m vllm.entrypoints.openai.api_server \
    --model microsoft/DialoGPT-medium \
    --port 8000 \
    --host 0.0.0.0
```

#### 3. 配置游戏
在 `script.js` 中修改配置：
```javascript
const AI_CONFIG = {
    backend: 'vllm', // 改为 vllm
    vllm: {
        baseUrl: 'http://localhost:8000/v1',
        model: 'meta-llama/Llama-2-7b-chat-hf',
        apiKey: 'your-api-key' // 如果需要的话
    }
};
```

### 选项2：云端部署 vLLM

#### 使用 RunPod
1. 访问 [RunPod](https://runpod.io)
2. 创建 GPU 实例
3. 安装 vLLM
4. 启动服务
5. 获取公网 IP

#### 使用 Google Colab
```python
# 在 Colab 中运行
!pip install vllm
!python -m vllm.entrypoints.openai.api_server \
    --model meta-llama/Llama-2-7b-chat-hf \
    --port 8000 \
    --host 0.0.0.0
```

### 选项3：使用现成的 AI 服务

#### OpenAI API
```javascript
const AI_CONFIG = {
    backend: 'openai',
    openai: {
        apiKey: 'sk-your-openai-api-key',
        model: 'gpt-3.5-turbo'
    }
};
```

#### Claude API
```javascript
const AI_CONFIG = {
    backend: 'claude',
    claude: {
        apiKey: 'your-claude-api-key',
        model: 'claude-3-sonnet-20240229'
    }
};
```

#### Gemini API
```javascript
const AI_CONFIG = {
    backend: 'gemini',
    gemini: {
        apiKey: 'your-gemini-api-key',
        model: 'gemini-pro'
    }
};
```

## 🎯 AI 分析功能

### 1. 游戏模式分析
- 分析用户的游戏频率和时间模式
- 识别结果分布特征
- 发现有趣的游戏习惯

### 2. 结果预测
- 基于历史数据预测下次结果
- 提供置信度评估
- 趋势分析

### 3. 个性化洞察
- 游戏成就统计
- 个性化建议
- 有趣的发现

## 🔧 配置说明

### 修改 AI 后端
在 `script.js` 中找到 `AI_CONFIG` 对象：

```javascript
const AI_CONFIG = {
    // 选择后端: 'vllm', 'openai', 'claude', 'gemini', 'mock'
    backend: 'mock', // 改为你想要的后端
    
    // 配置对应的参数
    vllm: {
        baseUrl: 'http://localhost:8000/v1',
        model: 'your-model-name',
        apiKey: 'your-api-key'
    }
};
```

### 测试连接
1. 启动 vLLM 服务
2. 打开游戏
3. 玩几局游戏（至少3次）
4. 点击 AI 分析按钮
5. 查看控制台日志

## 📊 数据流程

```
用户游戏 → 保存历史记录 → AI分析请求 → vLLM推理 → 返回分析结果 → 显示给用户
```

## 🛠️ 故障排除

### 常见问题

1. **连接失败**
   - 检查 vLLM 服务是否启动
   - 确认端口号正确
   - 检查防火墙设置

2. **模型加载失败**
   - 确认模型名称正确
   - 检查 GPU 内存是否足够
   - 尝试更小的模型

3. **API 调用失败**
   - 检查 API 密钥
   - 确认网络连接
   - 查看控制台错误信息

### 调试模式
在浏览器控制台中查看详细日志：
- AI 请求和响应
- 错误信息
- 性能数据

## 🎮 使用体验

### 新用户
- 需要至少3次游戏记录才能使用AI分析
- 会显示"需要更多数据"的提示

### 老用户
- 可以享受完整的AI分析功能
- 获得个性化的游戏洞察
- 有趣的预测和建议

## 🚀 部署到生产环境

### 安全考虑
- 使用 HTTPS
- 设置 API 密钥
- 限制请求频率
- 监控使用情况

### 性能优化
- 使用缓存
- 批量处理请求
- 优化模型大小
- 负载均衡

## 📈 扩展功能

### 可以添加的功能
- 多语言支持
- 更复杂的分析算法
- 实时数据流
- 用户反馈系统
- 分析历史记录

现在你的掷硬币游戏已经是一个完整的 AI 驱动的智能游戏了！🎯
