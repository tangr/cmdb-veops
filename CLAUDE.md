# CMDB 项目说明

这是维易CMDB（配置管理数据库）项目，一个简洁、轻量且高度可定制的运维配置管理数据库系统。

## 项目结构

- `cmdb-api/` - 后端API服务 (Python Flask)
- `cmdb-ui/` - 前端UI (Vue.js)
- `docs/` - 文档和配置文件
- `docker/` - Docker镜像构建文件

## 技术栈

### 后端

- Python 3.8-3.11
- Flask 2.2.5 + Gunicorn
- MySQL + Redis
- Celery (异步任务)
- Elasticsearch (可选)

### 前端

- Vue.js 2.6.11
- Ant Design Vue + Element UI
- ECharts (图表)
- Vuex + Vue Router

## 快速启动

### Docker 部署 (推荐)

```bash
# 克隆项目
git clone https://github.com/veops/cmdb.git
cd cmdb

# 启动服务
docker compose up -d
```

访问: <http://127.0.0.1:8000>

- 用户名: demo 或 admin
- 密码: 123456

### 本地开发

#### 后端API开发

```bash
cd cmdb-api

# 安装依赖
pip install -r requirements.txt

# 配置数据库
cp settings.example.py settings.py
# 编辑 settings.py 配置数据库连接

# 数据库迁移
flask db upgrade

# 启动开发服务器
flask run
```

#### 前端UI开发

```bash
cd cmdb-ui

# 安装依赖
npm install

# 启动开发服务器
npm run serve
```

## 常用命令

### 后端命令

```bash
# 数据库操作
flask db-setup                    # 初始化数据库
flask db upgrade                  # 数据库迁移
flask cmdb-init-cache            # 初始化缓存
flask cmdb-init-acl              # 初始化权限

# 开发工具
flask run                        # 启动开发服务器
python -m pytest tests/         # 运行测试
ruff check                       # 代码检查
```

### 前端命令

```bash
# 开发
npm run serve                    # 启动开发服务器
npm run build                    # 构建生产版本
npm run lint                     # 代码检查
npm test                         # 运行测试
```

### Docker命令

```bash
# 服务管理
docker compose up -d             # 启动所有服务
docker compose down              # 停止所有服务
docker compose logs -f           # 查看日志
docker compose ps                # 查看服务状态

# 重新构建
docker compose build             # 重新构建镜像
docker compose up -d --build     # 重新构建并启动
```

## 开发指南

### 代码规范

- 后端遵循 PEP 8 规范，使用 ruff 进行代码检查
- 前端使用 ESLint + Prettier 进行代码规范化
- 代码注释使用英文
- 代码格式化：输出空行中不要多余的空格，仅无空格的空行，输出文件末尾包含换行符

### 测试

- 后端测试: `pytest tests/`
- 前端测试: `npm run test:unit`

### 数据库

- 开发环境建议使用 MySQL 5.7+
- Redis 用于缓存和 Celery 任务队列
- 使用 Flask-Migrate 进行数据库版本管理

## 主要功能模块

- **CI管理** - 配置项和配置项类型管理
- **关系管理** - CI之间的关系定义和管理
- **自动发现** - 自动发现IT资产
- **权限控制** - 基于ACL的细粒度权限管理
- **IPAM** - IP地址管理
- **DCIM** - 数据中心基础设施管理
- **拓扑视图** - 资源关系可视化

## 环境变量

主要环境变量配置（见 `.env` 文件）:

- `MYSQL_ROOT_PASSWORD` - MySQL root密码
- `MYSQL_DATABASE` - 数据库名
- `REDIS_PASSWORD` - Redis密码
- `SECRET_KEY` - Flask密钥

## 故障排除

### 常见问题

1. **数据库连接失败**: 检查数据库配置和网络连接
2. **Redis连接失败**: 确认Redis服务正常运行
3. **前端访问404**: 检查Nginx配置和API服务状态
4. **权限问题**: 运行 `flask cmdb-init-acl` 初始化权限

### 日志查看

- API日志: `docker compose logs -f cmdb-api`
- UI日志: `docker compose logs -f cmdb-ui`
- 数据库日志: `docker compose logs -f cmdb-db`

## 相关链接

- 官方文档: <https://veops.cn/docs/>
- 在线体验: <https://cmdb.veops.cn>
- GitHub: <https://github.com/veops/cmdb>
- 问题反馈: <https://github.com/veops/cmdb/issues>
