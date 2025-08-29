# 🎯 智能掷硬币游戏

一个功能完整的掷硬币游戏，集成了用户系统、游戏历史记录和AI智能分析功能。

## ✨ 功能特点

### 🎮 核心游戏功能
- **3D翻转动画**：流畅的硬币翻转效果
- **随机结果生成**：真正的随机正面/反面结果
- **实时统计**：正面/反面次数实时更新
- **音效支持**：翻转时的音效反馈

### 👤 用户系统
- **用户注册**：支持用户名、邮箱、密码注册
- **用户登录**：安全的登录验证
- **数据持久化**：用户数据保存到JSONBin.io数据库
- **会话管理**：登录状态保持和退出功能

### 📊 游戏历史
- **历史记录**：保存每次游戏的详细记录
- **统计分析**：显示游戏频率和结果分布
- **数据同步**：支持多设备数据同步
- **本地备份**：网络失败时使用本地存储

### 🤖 AI智能分析
- **游戏模式分析**：识别用户的游戏习惯和模式
- **结果预测**：基于历史数据的智能预测
- **个性化洞察**：提供游戏建议和成就系统
- **多后端支持**：支持Transformers.js、Ollama、vLLM等

## 🚀 技术栈

- **前端**：HTML5, CSS3, JavaScript (ES6+)
- **数据库**：JSONBin.io (免费云数据库)
- **AI分析**：Transformers.js (浏览器内AI)
- **部署**：支持Netlify, Vercel, GitHub Pages

## 📁 项目结构

```
web-game/
├── index.html              # 主页面
├── style.css               # 样式文件
├── script.js               # 游戏逻辑和AI分析
├── README.md               # 项目说明
├── .gitignore              # Git忽略文件
├── DATABASE_SETUP.md       # 数据库配置指南
├── VLLM_COLAB_GUIDE.md     # vLLM部署指南
├── VLLM_SETUP.md           # vLLM设置说明
└── TRANSFORMERS_GUIDE.md   # Transformers.js指南
```

## 🎯 快速开始

### 1. 克隆项目
```bash
git clone https://github.com/your-username/coin-flip-game.git
cd coin-flip-game
```

### 2. 打开游戏
直接在浏览器中打开 `index.html` 文件即可开始游戏！

### 3. 开始游戏
1. 注册新账号或使用演示账号
2. 点击硬币开始游戏
3. 享受AI智能分析功能

## 🔧 配置说明

### 数据库配置（可选）
游戏默认使用本地存储，如需使用在线数据库：

1. 注册 [JSONBin.io](https://jsonbin.io) 账号
2. 创建新的Bin
3. 获取API密钥和Bin ID
4. 在 `script.js` 中更新配置：

```javascript
const JSONBIN_API_KEY = 'your-api-key';
const JSONBIN_BIN_ID = 'your-bin-id';
```

### AI分析配置
游戏支持多种AI后端：

#### Transformers.js（默认，推荐）
```javascript
const AI_CONFIG = {
    backend: 'transformers',
    transformers: {
        model: 'Xenova/distilbert-base-uncased',
        task: 'text-generation',
        maxLength: 200
    }
};
```

#### Ollama（本地AI）
```javascript
const AI_CONFIG = {
    backend: 'ollama',
    ollama: {
        baseUrl: 'http://localhost:11434',
        model: 'tinyllama'
    }
};
```

## 🌐 部署选项

### 方案1：Netlify Drop（最简单）
1. 访问 [netlify.com/drop](https://app.netlify.com/drop)
2. 拖拽整个项目文件夹
3. 获得在线链接

### 方案2：Vercel
1. 访问 [vercel.com](https://vercel.com)
2. 连接GitHub仓库
3. 自动部署

### 方案3：GitHub Pages
1. 推送代码到GitHub
2. 在仓库设置中启用GitHub Pages
3. 选择部署分支

### 方案4：其他静态托管
- Firebase Hosting
- Surge.sh
- Netlify
- Vercel

## 🎮 游戏玩法

### 基本操作
- **点击硬币**：开始翻转
- **空格键**：快速翻转
- **触摸设备**：支持触摸操作

### AI分析功能
- **🔍 分析游戏模式**：识别游戏习惯
- **🔮 预测下次结果**：基于历史数据预测
- **💡 获取游戏洞察**：个性化建议和成就

### 演示账号
- **玩家1**：`player1` / `123456`
- **玩家2**：`player2` / `123456`

## 📊 数据存储

### 用户数据结构
```json
{
  "username": "用户名",
  "email": "邮箱",
  "password": "密码",
  "createdAt": "注册时间",
  "gameStats": {
    "totalFlips": 0,
    "headsCount": 0,
    "tailsCount": 0,
    "lastPlayTime": null,
    "lastResult": null
  },
  "gameHistory": [
    {
      "id": 时间戳,
      "result": "正面/反面",
      "headsCount": 正面次数,
      "tailsCount": 反面次数,
      "totalFlips": 总翻转次数,
      "timestamp": "ISO时间",
      "playTime": "可读时间"
    }
  ]
}
```

## 🔒 隐私和安全

- **数据加密**：密码在传输中加密
- **本地优先**：数据优先保存在本地
- **用户控制**：用户可以随时删除数据
- **无追踪**：不收集用户行为数据

## 🛠️ 开发指南

### 本地开发
1. 克隆项目
2. 使用本地服务器（推荐）：
   ```bash
   # Python
   python -m http.server 8000
   
   # Node.js
   npx serve .
   
   # PHP
   php -S localhost:8000
   ```

### 添加新功能
1. 修改 `script.js` 添加游戏逻辑
2. 更新 `style.css` 添加样式
3. 在 `index.html` 中添加UI元素

### 自定义AI分析
在 `script.js` 中修改 `getMockAnalysis` 函数来自定义分析逻辑。

## 📈 性能优化

- **懒加载**：AI模型按需加载
- **缓存机制**：模型和结果缓存
- **压缩资源**：CSS和JS文件压缩
- **CDN加速**：使用CDN加载外部资源

## 🐛 故障排除

### 常见问题

#### AI分析不工作
- 检查网络连接
- 确认浏览器支持WebGL
- 查看控制台错误信息

#### 数据不同步
- 检查JSONBin.io配置
- 确认API密钥正确
- 使用同步按钮强制同步

#### 游戏卡顿
- 关闭其他标签页
- 检查浏览器内存使用
- 使用更轻量的AI模型

## 🤝 贡献指南

欢迎贡献代码！请遵循以下步骤：

1. Fork 项目
2. 创建功能分支：`git checkout -b feature/new-feature`
3. 提交更改：`git commit -am 'Add new feature'`
4. 推送分支：`git push origin feature/new-feature`
5. 提交Pull Request

## 📄 许可证

MIT License - 详见 [LICENSE](LICENSE) 文件

## 🙏 致谢

- [Transformers.js](https://github.com/xenova/transformers.js) - 浏览器内AI
- [JSONBin.io](https://jsonbin.io) - 免费数据库服务
- [Netlify](https://netlify.com) - 静态网站托管

## 📞 联系方式

- **GitHub Issues**：报告问题和建议
- **Email**：your-email@example.com

---

**享受你的智能掷硬币游戏！** 🎯🎮✨
