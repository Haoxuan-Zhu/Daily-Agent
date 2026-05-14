# Daily-Agent

一个用于记录实习每日日报与业务收获的 AI 辅助工具，支持自动生成学习摘要与图片识别分析。

## 功能特性

- **日报管理**：创建、查看、编辑和删除每日学习记录
- **日历视图**：通过日历组件直观查看和管理历史记录
- **AI 智能摘要**：调用 GLM-4 自动生成每日学习摘要
- **智能标签推荐**：根据内容自动推荐相关标签
- **图片识别分析**：使用 GLM-4V 分析图片内容并生成文字描述
- **数据统计**：查看总记录数与标签分布统计

## 技术栈

### 后端
- [FastAPI](https://fastapi.tiangolo.com/) 0.115.0 - Web 框架
- [SQLAlchemy](https://www.sqlalchemy.org/) 2.0.35 - ORM
- [Pydantic](https://docs.pydantic.dev/) 2.9.2 - 数据验证
- [MySQL](https://www.mysql.com/) + PyMySQL - 数据库
- [GLM-4](https://open.bigmodel.cn/) - AI 大模型 API
- 可选 [Redis](https://redis.io/) - 限流存储

### 前端
- [Next.js](https://nextjs.org/) 16.2.6 - React 框架
- [React](https://react.dev/) 19.2.4 - UI 库
- [TypeScript](https://www.typescriptlang.org/) - 类型安全
- [Tailwind CSS](https://tailwindcss.com/) - 样式

### 数据库
- MySQL

## 项目结构

```
.
├── intern-agent/
│   ├── backend/          # FastAPI 后端
│   │   ├── main.py       # 应用入口与 API 路由
│   │   ├── db.py         # 数据库模型与连接
│   │   ├── schemas.py    # Pydantic 数据模型
│   │   ├── agent.py      # AI 服务调用
│   │   ├── auth.py       # API Key 认证
│   │   ├── requirements.txt
│   │   └── .env.example  # 配置模板
│   ├── frontend/         # Next.js 前端
│   │   ├── app/          # 应用路由与页面
│   │   ├── package.json
│   │   └── tsconfig.json
│   ├── data/             # 数据目录
│   ├── start.sh          # 一键启动脚本
│   └── stop.sh           # 停止脚本
└── README.md
```

## 快速开始

### 环境要求
- Python 3.8+
- Node.js 18+
- MySQL 5.7+
- 可选：Redis

### 1. 克隆仓库

```bash
git clone https://github.com/Haoxuan-Zhu/-Agent.git
cd -Agent
```

### 2. 后端配置与启动

```bash
cd intern-agent/backend

# 安装依赖
pip install -r requirements.txt

# 配置环境变量
cp .env.example .env
# 编辑 .env，填入数据库密码、GLM API Key 等

# 启动服务
python main.py
```

后端默认运行在 `http://localhost:8000`，API 文档地址：`http://localhost:8000/docs`。

### 3. 前端配置与启动

```bash
cd intern-agent/frontend

# 安装依赖
npm install

# 启动开发服务器
npm run dev
```

前端默认运行在 `http://localhost:3000`。

### 一键启动（推荐）

```bash
cd intern-agent
./start.sh
```

## 环境变量

| 变量名 | 说明 | 默认值 |
|---|---|---|
| `DATABASE_URL` | MySQL 连接地址 | - |
| `API_KEY` | API 认证密钥 | - |
| `GLM_API_KEY` | 智谱 AI API Key | - |
| `GLM_MODEL` | GLM 模型名称 | `glm-4` |
| `REDIS_URL` | Redis 地址（可选） | `redis://localhost:6379` |
| `ALLOWED_ORIGINS` | CORS 允许的源 | `http://localhost:3000` |
| `HOST` | 服务监听地址 | `0.0.0.0` |
| `PORT` | 服务端口 | `8000` |

## API 概览

| 方法 | 路径 | 说明 |
|---|---|---|
| GET | `/health` | 健康检查 |
| POST | `/logs` | 创建学习记录 |
| GET | `/logs` | 获取记录列表 |
| GET | `/logs/{id}` | 获取单条记录 |
| PUT | `/logs/{id}` | 更新记录 |
| DELETE | `/logs/{id}` | 删除记录 |
| GET | `/logs/stats/summary` | 统计摘要 |
| POST | `/recognize-image` | 图片识别 |

## 安全特性

- API Key 认证
- 请求限流（slowapi）
- CORS 来源限制
- 输入数据校验（Pydantic）
- 全局异常处理，不暴露内部信息
- 结构化日志记录

## 开发计划

- [ ] AI 摘要异步任务处理
- [ ] Redis 缓存层
- [ ] 更多数据可视化图表
- [ ] 导出日报为 PDF/Word

## License

MIT
