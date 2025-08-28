# Google Colab + vLLM 完整部署指南

## 🎯 概述

本指南将帮助你在Google Colab上部署vLLM，并将其集成到你的掷硬币游戏中，提供真实的AI分析功能。

## 📋 前置要求

- Google账号
- Colab Pro订阅 ($10/月) - 推荐
- 稳定的网络连接

## 🚀 部署步骤

### 步骤1：打开Google Colab

1. 访问 [colab.research.google.com](https://colab.research.google.com)
2. 登录你的Google账号
3. 点击"New notebook"
4. 重命名为"vllm-coin-game"

### 步骤2：升级到Colab Pro（推荐）

1. 点击右上角"Upgrade"
2. 选择"Colab Pro" ($10/月)
3. 完成支付

**为什么需要Pro？**
- 更长的GPU时间
- 更稳定的连接
- 更好的性能

### 步骤3：创建Cell 1 - 安装依赖和下载模型

点击"+"按钮，选择"Code"，输入以下代码：

```python
# Cell 1: 并行安装依赖和下载模型
import subprocess
import threading
import time

def install_dependencies():
    print("🔧 开始安装依赖...")
    subprocess.run(['pip', 'install', 'vllm', 'transformers', 'torch', 'pyngrok'])
    print("✅ 依赖安装完成！")

def download_model():
    print("📥 开始下载模型...")
    from transformers import AutoTokenizer
    try:
        tokenizer = AutoTokenizer.from_pretrained('meta-llama/Llama-2-7b-chat-hf')
        print("✅ Llama-2模型下载完成！")
    except Exception as e:
        print(f"❌ Llama-2下载失败: {e}")
        print("🔄 尝试使用备用模型...")
        tokenizer = AutoTokenizer.from_pretrained('microsoft/DialoGPT-medium')
        print("✅ 备用模型下载完成！")

def check_gpu():
    print("🖥️ 检查GPU状态...")
    subprocess.run(['nvidia-smi'])

# 并行执行安装和下载
print("🚀 开始并行安装和下载...")
thread1 = threading.Thread(target=install_dependencies)
thread2 = threading.Thread(target=download_model)
thread3 = threading.Thread(target=check_gpu)

thread1.start()
thread2.start()
thread3.start()

# 等待所有任务完成
thread1.join()
thread2.join()
thread3.join()

print("🎉 所有任务完成！")
```

**运行时间：** 10-15分钟

### 步骤4：创建Cell 2 - 启动vLLM服务

```python
# Cell 2: 启动vLLM服务
import subprocess
import threading
import time
import os

def start_vllm():
    try:
        print("🚀 启动vLLM服务...")
        subprocess.run([
            'python', '-m', 'vllm.entrypoints.openai.api_server',
            '--model', 'meta-llama/Llama-2-7b-chat-hf',
            '--port', '8000',
            '--host', '0.0.0.0',
            '--max-model-len', '2048'
        ])
    except Exception as e:
        print(f"❌ Llama-2启动失败: {e}")
        print("🔄 尝试使用备用模型...")
        try:
            subprocess.run([
                'python', '-m', 'vllm.entrypoints.openai.api_server',
                '--model', 'microsoft/DialoGPT-medium',
                '--port', '8000',
                '--host', '0.0.0.0'
            ])
        except Exception as e2:
            print(f"❌ 备用模型也启动失败: {e2}")

print("🔄 启动vLLM服务...")
vllm_thread = threading.Thread(target=start_vllm)
vllm_thread.daemon = True
vllm_thread.start()

# 等待服务启动
print("⏳ 等待服务启动...")
for i in range(30):
    print(f"等待中... {i+1}/30")
    time.sleep(2)
    
print("✅ vLLM服务应该已经启动！")
```

**运行时间：** 5-10分钟

### 步骤5：创建Cell 3 - 暴露端口

```python
# Cell 3: 使用ngrok暴露端口
from pyngrok import ngrok
import time

print("🌐 正在暴露端口...")
try:
    # 暴露8000端口
    public_url = ngrok.connect(8000)
    print("✅ 端口暴露成功！")
    print("=" * 60)
    print(f"🔗 Public URL: {public_url}")
    print(f"🔗 API URL: {public_url}/v1")
    print("=" * 60)
    print("📋 重要：请复制上面的URL到你的游戏配置中！")
    print("=" * 60)
    
    # 保存URL到变量，供下一个Cell使用
    globals()['ngrok_url'] = str(public_url)
    
except Exception as e:
    print(f"❌ 暴露端口失败: {e}")
    print("请检查ngrok是否正确安装")
```

### 步骤6：创建Cell 4 - 测试服务

```python
# Cell 4: 测试vLLM服务
import requests
import json
import time

# 等待一下让服务完全启动
print("⏳ 等待服务完全启动...")
time.sleep(10)

# 测试API
test_url = f"{ngrok_url}/v1/chat/completions"
test_data = {
    "model": "meta-llama/Llama-2-7b-chat-hf",
    "messages": [
        {"role": "user", "content": "Hello, how are you?"}
    ],
    "max_tokens": 50
}

print("🧪 测试vLLM服务...")
try:
    response = requests.post(test_url, json=test_data, timeout=30)
    if response.status_code == 200:
        print("✅ vLLM服务运行正常！")
        result = response.json()
        ai_reply = result['choices'][0]['message']['content']
        print(f"🤖 AI回复: {ai_reply}")
        print("🎉 服务测试成功！可以开始使用AI分析功能了！")
    else:
        print(f"❌ 服务测试失败: {response.status_code}")
        print(f"响应: {response.text}")
except Exception as e:
    print(f"❌ 连接失败: {str(e)}")
    print("请检查服务是否正常启动")
```

## 🔧 配置游戏

### 修改script.js文件

在 `script.js` 中找到 `AI_CONFIG` 对象，修改为：

```javascript
const AI_CONFIG = {
    // 选择AI后端: 'vllm', 'openai', 'claude', 'gemini', 'mock'
    backend: 'vllm', // 使用Colab的vLLM服务
    
    // vLLM配置
    vllm: {
        baseUrl: 'https://YOUR_NGROK_URL/v1', // 替换为你的ngrok URL
        model: 'meta-llama/Llama-2-7b-chat-hf', // 或你使用的模型名
        apiKey: 'your-vllm-api-key' // 通常不需要
    }
};
```

**重要：** 将 `YOUR_NGROK_URL` 替换为Cell 3中显示的ngrok URL

### 示例配置

```javascript
// 示例：如果你的ngrok URL是 https://abc123.ngrok.io
vllm: {
    baseUrl: 'https://abc123.ngrok.io/v1',
    model: 'meta-llama/Llama-2-7b-chat-hf',
    apiKey: 'your-vllm-api-key'
}
```

## 🎮 测试游戏

1. 打开你的掷硬币游戏
2. 注册/登录账号
3. 玩几局游戏（至少3次）
4. 点击AI分析按钮
5. 查看是否连接成功

## ⚠️ 重要注意事项

### Colab限制
- **会话时间**：最长12小时
- **GPU时间**：每天有限制
- **网络**：可能不稳定

### 解决方案
- **保存notebook**：定期保存代码
- **监控时间**：避免超时
- **备用方案**：准备其他AI服务

### 成本
- **Colab Pro**：$10/月
- **GPU时间**：每天最多12小时
- **适合**：学习和实验

## 🛠️ 故障排除

### 常见问题

#### 1. 模型下载失败
```python
# 使用更小的模型
tokenizer = AutoTokenizer.from_pretrained('microsoft/DialoGPT-medium')
```

#### 2. 服务启动失败
```python
# 检查GPU内存
!nvidia-smi

# 使用更小的模型
subprocess.run([
    'python', '-m', 'vllm.entrypoints.openai.api_server',
    '--model', 'microsoft/DialoGPT-medium',
    '--port', '8000',
    '--host', '0.0.0.0'
])
```

#### 3. 连接失败
- 检查ngrok URL是否正确
- 确认Colab notebook还在运行
- 查看控制台错误信息

#### 4. 游戏无法连接
- 确认script.js中的URL正确
- 检查CORS设置
- 查看浏览器控制台错误

### 调试命令

```python
# 检查GPU状态
!nvidia-smi

# 检查端口占用
!netstat -tlnp | grep 8000

# 检查进程
!ps aux | grep vllm

# 测试本地连接
!curl http://localhost:8000/v1/models
```

## 📊 性能优化

### 模型选择
- **Llama-2-7b**：功能强大，需要更多资源
- **DialoGPT-medium**：轻量级，适合测试

### 参数调整
```python
# 减少内存使用
'--max-model-len', '1024'  # 减少到1024

# 使用更小的batch size
'--max-num-batched-tokens', '2048'
```

## 🔄 重启服务

如果服务出现问题，可以重新运行Cell 2-4：

1. 停止当前服务（Ctrl+C）
2. 重新运行Cell 2（启动服务）
3. 重新运行Cell 3（暴露端口）
4. 重新运行Cell 4（测试服务）

## 📈 监控和维护

### 监控服务状态
```python
# 检查服务健康状态
import requests
try:
    response = requests.get(f"{ngrok_url}/v1/models")
    if response.status_code == 200:
        print("✅ 服务运行正常")
    else:
        print("❌ 服务异常")
except:
    print("❌ 无法连接到服务")
```

### 保存重要信息
```python
# 保存配置信息
config_info = {
    'ngrok_url': ngrok_url,
    'model': 'meta-llama/Llama-2-7b-chat-hf',
    'timestamp': time.time()
}

print("📋 配置信息:")
for key, value in config_info.items():
    print(f"{key}: {value}")
```

## 🎯 总结

通过这个指南，你可以：

1. ✅ 在Google Colab上部署vLLM
2. ✅ 将AI服务集成到你的游戏中
3. ✅ 享受真实的AI分析功能
4. ✅ 节省本地计算资源

**总成本：** $10/月（Colab Pro）
**部署时间：** 20-30分钟
**维护难度：** 中等

现在你的掷硬币游戏已经是一个完整的AI驱动的智能游戏了！🎮🤖
