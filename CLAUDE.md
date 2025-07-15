# Social Media Cognitive Analysis System

一个基于AI的社交媒体内容分析系统，用于分析微博博主和微信公众号的认知规律，提升分析能力和预测准确性。

## 项目概述

### 核心功能
- 自动化采集微博和微信公众号内容
- 多AI模型支持（OpenAI、DeepSeek、Gemini等）
- 博主认知规律分析和建模
- 基于历史数据的趋势预测
- 上下文持续化学习

### 技术栈
- **后端**: Python 3.11/3.12 + FastAPI
- **前端**: Vue.js + Element UI
- **数据库**: SQLite (开发) / PostgreSQL (生产)
- **浏览器自动化**: Selenium + ChromeDriver
- **AI集成**: 多厂商API统一接口

## 快速开始

### 环境要求
- Python 3.11 或 3.12
- Chrome浏览器
- 至少一个AI模型的API Key

### 安装步骤

```bash
# 克隆项目
git clone https://github.com/yourusername/social-media-cognitive-analysis.git
cd social-media-cognitive-analysis

# 创建虚拟环境
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate

# 安装依赖
pip install -r requirements.txt

# 初始化数据库
python scripts/init_db.py

# 启动应用
python main.py
```

### 基本配置

访问 `http://localhost:8000` 进行初始配置：

1. 设置AI模型API Keys
2. 配置微博/微信账号信息
3. 选择要分析的博主列表

## 系统架构

### 模块组织

```
social-media-cognitive-analysis/
├── app/
│   ├── core/           # 核心配置和工具
│   ├── api/            # API路由
│   ├── services/       # 业务逻辑
│   ├── models/         # 数据模型
│   ├── scrapers/       # 数据采集
│   └── analyzers/      # AI分析引擎
├── frontend/           # 前端代码
├── data/              # 数据存储
├── logs/              # 日志文件
├── scripts/           # 工具脚本
└── tests/             # 测试代码
```

### 数据流程

1. **数据采集** → 浏览器自动化获取内容
2. **数据清洗** → 结构化存储到数据库
3. **AI分析** → 多模型并行分析
4. **上下文管理** → 持续化学习和更新
5. **预测生成** → 基于历史数据预测趋势

## 核心功能详解

### 1. 数据采集模块

#### 微博采集
```python
# 配置微博登录信息
weibo_config = {
    "username": "your_username",
    "password": "your_password",
    # 或使用token
    "token": "your_access_token"
}

# 选择博主进行采集
bloggers = ["博主1", "博主2", "博主3"]
```

#### 微信公众号采集
```python
# 配置公众号信息
wechat_config = {
    "accounts": ["公众号1", "公众号2"]
}
```

### 2. AI分析引擎

#### 支持的AI模型
- **OpenAI**: GPT-4, GPT-3.5-turbo
- **DeepSeek**: deepseek-chat, deepseek-coder
- **Gemini**: gemini-pro, gemini-pro-vision
- **其他兼容模型**: 支持OpenAI API格式的模型

#### 模型配置
```python
ai_models = {
    "openai": {
        "api_key": "your_openai_key",
        "model": "gpt-4",
        "base_url": "https://api.openai.com/v1"
    },
    "deepseek": {
        "api_key": "your_deepseek_key",
        "model": "deepseek-chat",
        "base_url": "https://api.deepseek.com/v1"
    }
}
```

### 3. 认知分析功能

#### 分析维度
- **情感倾向**: 正面、负面、中性情感分析
- **观点变化**: 追踪博主观点演变轨迹
- **话题偏好**: 识别关注的核心话题
- **表达风格**: 分析语言模式和修辞特点
- **互动模式**: 分析与粉丝的互动规律

#### 上下文持续化
```python
# 上下文管理示例
context_manager = {
    "blogger_id": "blogger_123",
    "historical_analysis": [...],  # 历史分析结果
    "cognitive_model": {...},      # 认知模型参数
    "last_update": "2024-01-15"
}
```

### 4. 预测功能

#### 预测类型
- **内容趋势**: 预测博主未来可能发布的内容类型
- **情感走势**: 预测情感倾向的变化趋势
- **话题热度**: 预测关注话题的热度变化
- **行为模式**: 预测发布频率和时间规律

#### 预测增强
- **联网搜索**: 结合实时信息优化预测
- **多博主关联**: 分析博主间的影响关系
- **事件驱动**: 基于突发事件调整预测模型

## API文档

### 核心API接口

#### 博主管理
```http
POST /api/bloggers          # 添加博主
GET /api/bloggers           # 获取博主列表
PUT /api/bloggers/{id}      # 更新博主信息
DELETE /api/bloggers/{id}   # 删除博主
```

#### 内容采集
```http
POST /api/scraping/start    # 开始采集
GET /api/scraping/status    # 获取采集状态
POST /api/scraping/stop     # 停止采集
```

#### 分析任务
```http
POST /api/analysis/start    # 开始分析
GET /api/analysis/results   # 获取分析结果
GET /api/analysis/history   # 获取历史分析
```

#### 预测功能
```http
POST /api/prediction/generate   # 生成预测
GET /api/prediction/results     # 获取预测结果
```

## 配置说明

### 环境变量配置

创建 `.env` 文件：

```env
# 数据库配置
DATABASE_URL=sqlite:///./data/app.db

# AI模型配置
OPENAI_API_KEY=your_openai_key
DEEPSEEK_API_KEY=your_deepseek_key
GEMINI_API_KEY=your_gemini_key

# 微博配置
WEIBO_USERNAME=your_username
WEIBO_PASSWORD=your_password

# 应用配置
DEBUG=True
SECRET_KEY=your_secret_key
```

### 系统配置

```python
# config/settings.py
SCRAPING_CONFIG = {
    "delay_range": (2, 5),      # 请求间隔（秒）
    "max_retries": 3,           # 最大重试次数
    "timeout": 30,              # 请求超时时间
    "concurrent_tasks": 3       # 并发任务数
}

ANALYSIS_CONFIG = {
    "batch_size": 10,           # 批量分析大小
    "context_window": 100,      # 上下文窗口大小
    "model_rotation": True      # 是否轮换使用模型
}
```

## 高级功能

### 自定义分析模板

```python
# 创建分析模板
analysis_template = {
    "name": "情感分析模板",
    "prompt": "分析以下内容的情感倾向和关键观点：{content}",
    "model": "gpt-4",
    "parameters": {
        "temperature": 0.7,
        "max_tokens": 500
    }
}
```

### 插件系统

```python
# 自定义分析插件
class CustomAnalysisPlugin:
    def analyze(self, content, context):
        # 自定义分析逻辑
        return analysis_result
    
    def predict(self, historical_data):
        # 自定义预测逻辑
        return prediction_result
```

### 数据导出

```python
# 导出分析结果
export_formats = ["JSON", "CSV", "Excel", "PDF报告"]
```

## 部署指南

### 开发环境
```bash
# 直接运行
python main.py
```

### 生产环境
```bash
# 使用Docker
docker build -t social-media-analysis .
docker run -p 8000:8000 social-media-analysis

# 或使用Docker Compose
docker-compose up -d
```

### 性能优化
- 使用Redis进行缓存
- 配置数据库连接池
- 启用异步任务队列
- 设置负载均衡

## 安全考虑

### 数据保护
- API Keys加密存储
- 敏感信息环境变量管理
- 数据传输HTTPS加密
- 定期备份重要数据

### 合规性
- 遵守平台ToS
- 实施请求频率限制
- 用户数据隐私保护
- 审计日志记录

## 故障排除

### 常见问题

**Q: 浏览器自动化失败**
A: 检查ChromeDriver版本是否与Chrome浏览器匹配，确保系统PATH配置正确。

**Q: AI模型调用失败**
A: 验证API Key是否正确，检查网络连接和API配额限制。

**Q: 数据采集被阻止**
A: 适当增加请求间隔，检查User-Agent和Cookie配置。

**Q: 分析结果不准确**
A: 调整分析模板和参数，增加上下文信息，考虑使用更强大的模型。

### 日志分析
```bash
# 查看系统日志
tail -f logs/app.log

# 查看错误日志
tail -f logs/error.log

# 查看采集日志
tail -f logs/scraping.log
```

## 贡献指南

### 开发流程
1. Fork项目并创建特性分支
2. 编写代码和测试
3. 提交Pull Request
4. 代码审查和合并

### 代码规范
- 遵循PEP 8编码规范
- 添加必要的类型注解
- 编写单元测试
- 更新相关文档

## 许可证

MIT License - 详见 [LICENSE](LICENSE) 文件

## 支持

- 问题报告：[GitHub Issues](https://github.com/yourusername/social-media-cognitive-analysis/issues)
- 功能请求：[GitHub Discussions](https://github.com/yourusername/social-media-cognitive-analysis/discussions)
- 邮件支持：support@example.com

---

**注意**: 使用本系统进行数据采集时，请确保遵守相关平台的使用条款和法律法规。本项目仅供学习和研究使用。

